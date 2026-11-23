# D4 – Design

Návrh riešenia Light Potion: architektúra, protokol Bluetooth, firmvér, aplikácia a hardvér.

## 1. Architektúra systému

```text
 ┌──────────────── Telefón s Androidom ─────────────────┐            ┌──────────── Light Potion ────────────┐
 │                                                     │            │                                      │
 │  Notifikácia ──► NotificationListener               │            │  BLE služba ──► LED efekt ──► WS2812 │
 │                   │ iba category, flags, priority   │  2 bajty   │  (NimBLE)       (FastLED)            │
 │                   ▼                                 │ ─────────► │                                      │
 │               NotificationMapper ──► BleConnection- │ Bluetooth  │  ESP32-C3                            │
 │               [kategória, naliehavosť]   Manager    │     LE     │                                      │
 │                                                     │            │                                      │
 │  ConnectionService (služba v popredí) drží spojenie │            │                                      │
 └─────────────────────────────────────────────────────┘            └──────────────────────────────────────┘
```

Telefón robí všetko „rozmýšľanie“ (ktorá notifikácia je aká), zariadenie iba zobrazí farbu. Firmvér je preto jednoduchý a text notifikácií telefón nikdy neopustí.

Proces krok za krokom (diagram BPMN) a schéma zapojenia finálnej verzie sú na [webovej stránke v0.2](pathname:///knifes_overview/assets/Light_Potion_v0.2.html). Vzhľad je v [3D modeli](pathname:///knifes_overview/assets/Potion_Notifier_3D_model.html).

## 2. Protokol Bluetooth LE

Spoločná dohoda medzi firmvérom (`firmware/include/config.h`) a aplikáciou (`BleContract.kt`).

| Položka | Hodnota |
|---|---|
| Názov zariadenia | `LightPotion` |
| UUID služby | `4c50ff00-7a31-4e2b-9c5d-8f1a2b3c4d5e` |
| UUID charakteristiky | `4c50ff01-7a31-4e2b-9c5d-8f1a2b3c4d5e` |
| Vlastnosti | Write, Write Without Response |
| Obsah správy | presne 2 bajty: `[kategória, naliehavosť]` |

| Kategória | Význam | Farba |
|---|---|---|
| 0 | iné | biela |
| 1 | hovor | zelená |
| 2 | správa | modrá |
| 3 | e-mail | žltá |

Naliehavosť: `0` = normálna, `1` = vysoká.

Zariadenie vysiela UUID služby v reklamnom pakete a názov v odpovedi na skenovanie, pretože 128-bitové UUID zaberie takmer celý paket. Aplikácia hľadá zariadenie podľa UUID služby.

## 3. Firmvér

### Moduly

| Súbor | Zodpovednosť |
|---|---|
| `config.h` | Všetky nastaviteľné hodnoty: pin LED, počet LED, jas, časy animácie, farby, UUID |
| `ble_service.*` | Bluetooth služba, kontrola správy, opätovné vysielanie po odpojení |
| `led_effect.*` | Animácia blikania a zhasnutia, nezávislá od Bluetooth |
| `main.cpp` | Spojí moduly dokopy |

Animácia je oddelená od Bluetooth, aby sa dala neskôr použiť pre iné tvary a počty LED.

### Stavový automat animácie

```text
           platná správa                 po 1800 ms (naliehavá 2300 ms)
  NEČINNÝ ───────────────► BLIKANIE ─────────────────────────────► ZHASÍNANIE
     ▲                       │  každých 40–90 ms náhodný jas            │  plynulo z posledného jasu
     │                       │  30–100 % z limitu                       │  na 0 za 700 ms
     └───────────────────────┴──────────────────────────────────────────┘
                 nová správa počas animácie = začne odznova v novej farbe
```

- Animácia nikdy nepoužíva `delay()`, iba `millis()`, takže Bluetooth nie je nikdy blokované.
- Limit jasu: 80 z 255 pre normálnu notifikáciu, 255 pre naliehavú.
- Správa inej dĺžky ako 2 bajty alebo s neznámou hodnotou sa zahodí a do sériovej linky sa zapíše varovanie.

## 4. Aplikácia pre Android

### Moduly

| Balík | Zodpovednosť |
|---|---|
| `ble/` | Hľadanie zariadenia, pripojenie, fronta zápisov (`BleConnectionManager`), dohoda protokolu (`BleContract`) |
| `notify/` | Čítanie notifikácií (`LightPotionNotificationListener`) a mapovanie na kategórie (`NotificationMapper`, čistá funkcia s testami) |
| `service/` | Služba v popredí typu `connectedDevice`, ktorá drží spojenie |
| `ui/` | Obrazovky v Jetpack Compose |

### Mapovanie notifikácií

| Kategória v Androide | Bajt |
|---|---|
| `CATEGORY_CALL` | 1, vždy naliehavá |
| `CATEGORY_MESSAGE`, `CATEGORY_SOCIAL` | 2 |
| `CATEGORY_EMAIL` | 3 |
| všetko ostatné | 0 |

Naliehavosť je 1 pre hovor alebo pre notifikáciu s vysokou či maximálnou prioritou. Úplne sa preskočia trvalé notifikácie (hudba, navigácia), súhrny skupín a notifikácie samotnej aplikácie.

### Pripojenie

Jedna korutina beží v slučke: hľadanie → pripojenie → posielanie. Pri chybe čaká 1 s, potom 2 s, 4 s… najviac 30 s a skúsi to znova. Pri známej chybe GATT 133 skúsi pripojenie ešte raz. Adresa zariadenia sa zapamätá. Zápisy idú najviac raz za 500 ms a ak ich príde viac, pošle sa iba najnovší.

### Obrazovky

1. **Nastavenie** – zoznam povolení: Bluetooth, notifikácie aplikácie, prístup k notifikáciám, výnimka z optimalizácie batérie (voliteľné). Tlačidlo Pokračovať je aktívne až po udelení povinných povolení.
2. **Domov** – stav spojenia (odpojené, hľadá, pripája sa, pripojené) s animovanou „guľou elixíru“, posledná odoslaná kategória a štyri testovacie tlačidlá: Call, Message, Email, Other.

### Súkromie

Aplikácia číta iba `category`, `flags` a `priority`. Nadpis, text, odosielateľa ani extras nikdy nečíta, neukladá, neposiela ani nezapisuje do logu. Nemá povolenie na internet a nepoužíva analytiku.

## 5. Hardvér

### Prototyp (aktuálny stav)

| Modul WS2812 | ESP32-C3 Super Mini |
|---|---|
| GND | G |
| 5V | 3V3 |
| DI | GPIO4 |

Napájanie z USB-C. GPIO2, GPIO8 a GPIO9 sa na LED nepoužívajú, lebo ovplyvňujú štart dosky a GPIO8 ovláda LED na doske. Ak by LED pri 3,3 V blikala alebo mala zlé farby, napájanie LED sa presunie na pin 5V a do dátového vodiča sa pridá rezistor 330 Ω.

### Finálna verzia (plánované)

- Seeed XIAO ESP32-C3, chránený LiPo 250 mAh, tlačidlo s aretáciou vo viečku medzi batériou a doskou.
- Tri LED WS2812B napájané cez P-MOSFET Q2 (AO3401), ktorý zapína N-MOSFET Q1 (2N7002) z GPIO3. GPIO3 vysoko = LED napájané, nízko = vypnuté.
- Dáta LED na GPIO4 cez 330 Ω. Pred vypnutím napájania LED firmvér nastaví GPIO4 nízko (R9).
- Kondenzátor 100 µF pri LED, port USB-C na spodku fľaštičky.

### Mechanický návrh

Fľaštička z matného materiálu široká asi 35 mm, korkové viečko s tlačidlom, mosadzná objímka s očkom na krúžok na kľúče. Tvar je prvý návrh, elektronika od neho nezávisí.

## 6. Odhad spotreby (overí sa meraním)

Pri pokojovom prúde asi 1 mA vydrží batéria 250 mAh asi 250 hodín, teda asi 10 dní. Po započítaní bliknutí a strát vychádza odhad asi 8 dní. Skutočná hodnota sa zmeria v míľniku M9 a podľa nej sa upraví interval Bluetooth spojenia.

## 7. Plánované zmeny návrhu

- Párovanie a šifrovanie Bluetooth (v kóde je pripravené miesto s poznámkou TODO).
- Dlhší interval spojenia pre nízku spotrebu.
- Správanie podľa stavu batérie (napríklad červené bliknutie pri slabej batérii).
- Nastavenia v aplikácii: filter podľa aplikácie, vlastné farby, tichý režim (v1.1).
- Podpora iPhonu cez ANCS (v2.0).

---
**Navigation:** [⬆️ Up](../index.md) · [🏠 Home](../index.md)
