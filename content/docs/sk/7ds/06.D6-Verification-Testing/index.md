# D6 – Verification & Testing

Overenie, či Light Potion spĺňa ciele E1–E7 a požiadavky z [D3](../03.D3-Analysis/index.md). Stav k 2026-11-23.

**Výsledok:** prototyp na nepájivom poli je otestovaný a funguje. Všetky testy prototypu (jednotkové testy, firmvér aj aplikácia) prešli. Neotestované ostávajú iba časti finálnej verzie, ktoré ešte neexistujú: batéria, tlačidlo vo viečku, nabíjanie a fľaštička.

**Legenda:** ✅ overené · 📅 plánované vo finálnej verzii

## 1. Jednotkové testy

*Zodpovedná: Lucia Kačmárová*

`NotificationMapperTest.kt` obsahuje 15 testov: každý riadok tabuľky mapovania kategórií, výpočet naliehavosti a pravidlá preskočenia (trvalé notifikácie, súhrny skupín, vlastné notifikácie).

```sh
cd android
./gradlew testDebugUnitTest
```

| Test | Stav |
|---|---|
| Kompilácia aplikácie (`assembleDebug`) | ✅ |
| 15 jednotkových testov mapovania | ✅ všetky prešli |
| Kompilácia a nahratie firmvéru (`pio run -t upload`) | ✅ |

## 2. Test firmvéru cez nRF Connect

*Zodpovedný: Filip Brutovský*

Postup je v `firmware/TESTING.md`. Do charakteristiky `4c50ff01-…` sa zapíše bajtové pole a sleduje sa LED a sériový výpis.

| ID | Vstup | Očakávaný výsledok | Stav |
|---|---|---|---|
| T1 | štart dosky | výpis `LightPotion fw 0.1.0`, `BLE advertising`, LED zhasnutá | ✅ |
| T2 | `0200` | modré blikanie asi 1,8 s a zhasnutie asi 0,7 s | ✅ (fotka v [D5](../05.D5-Implementation/index.md)) |
| T3 | `0100` | zelená, asi 2,5 s | ✅ |
| T4 | `0300` | žltá, asi 2,5 s | ✅ |
| T5 | `0000` | biela, asi 2,5 s | ✅ |
| T6 | `0201` | modrá, asi 3 s, plný jas | ✅ |
| T7 | `02`, `020000` | nič, varovanie o zlej dĺžke, doska beží ďalej | ✅ |
| T8 | `0900`, `0205` | nič, varovanie o zlej hodnote, doska beží ďalej | ✅ |
| T9 | odpojenie a nové pripojenie | doska znovu vysiela, ďalší zápis funguje | ✅ |
| T10 | `0300` počas bežiacej `0201` | animácia začne odznova na žlto, bez odpojenia | ✅ |

## 3. Test aplikácie

*Zodpovedná: Lucia Kačmárová*

Podrobný zoznam je v `android/TESTING.md`.

| ID | Test | Očakávaný výsledok | Stav |
|---|---|---|---|
| A1 | Prvé spustenie | zoznam povolení, Pokračovať až po povinných povoleniach | ✅ |
| A2 | Pripojenie | Scanning → Connecting → Connected | ✅ |
| A3 | Odpojenie a návrat dosky | aplikácia sa sama pripojí do asi 30 s | ✅ |
| A4 | Testovacie tlačidlá | Call zelená, Message modrá, Email žltá, Other biela | ✅ |
| A5 | Rýchle stláčanie | najviac jeden zápis za 500 ms | ✅ |
| A6 | Správa z WhatsAppu, Signalu alebo SMS | modrá | ✅ |
| A7 | E-mail | žltá | ✅ |
| A8 | Prichádzajúci hovor | zelená, dlhšie a jasnejšie | ✅ |
| A9 | Hudba, navigácia, súhrn skupiny, vlastná notifikácia | LED nereaguje | ✅ |
| A10 | Aplikácia zavretá zo zoznamu posledných | služba beží, LED stále reaguje | ✅ |
| A11 | `adb logcat` počas správ | žiadny text, nadpis ani odosielateľ | ✅ |
| A12 | Povolenia aplikácie | bez povolenia na internet | ✅ |

## 4. Overenie cieľov

| Cieľ | Ako sa overí | Stav |
|---|---|---|
| E1 Svetlo pri notifikácii | testy T2–T6, A4, A6–A8 | ✅ všetky štyri farby, testovacie tlačidlá aj skutočné notifikácie |
| E2 Oneskorenie do 2 s | od príchodu notifikácie po svetlo, zariadenie v dosahu | ✅ na prototype |
| E3 Výdrž aspoň 7 dní | meranie pokojového prúdu multimetrom a test vybitia | 📅 M9 |
| E4 Šírka asi 35 mm | meranie vytlačenej fľaštičky | 📅 M8 |
| E5 Tlačidlo na viečku | zapnutie a vypnutie batérie | 📅 M8 |
| E6 Nabíjanie cez USB-C | nabitie z vybitého stavu | 📅 M8 |
| E7 Súkromie | kontrola kódu, testy A11 a A12 | ✅ aplikácia číta iba category, flags a priority, v logoch nie je text notifikácií, bez povolenia na internet |

## 5. Plánované testy finálnej verzie

- Pokojový prúd s vypnutým MOSFETom (opatrenie M5) a s rôznym intervalom spojenia (M2).
- Skutočná výdrž batérie pri bežnom počte notifikácií za deň.
- Kontrola, že sa LED pri vypnutom napájaní nenapájajú cez dátový pin (R9).
- Test na dvoch značkách telefónov (opatrenie M1).
- Kontrola polarity batérie pred prvým pripojením (M4).

Tieto testy sa spravia po zložení finálnej verzie (míľniky M8 a M9) a výsledky sa doplnia do tabuľky cieľov.

---
**Navigation:** [⬆️ Up](../index.md) · [🏠 Home](../index.md)
