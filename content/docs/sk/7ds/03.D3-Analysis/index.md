# D3 – Analysis

## Existujúce riešenia

| Riešenie | Výhody | Nevýhody oproti Light Potion |
|---|---|---|
| Smart hodinky | Zobrazia aj text, veľa funkcií | Drahé, nabíjanie každý deň alebo dva, treba ich nosiť na ruke |
| Fitness náramok | Lacnejší, vibrácie | Treba ho nosiť, posiela aj text, nie je to dekoratívny predmet |
| Notifikačná LED na telefóne | Zadarmo | Väčšina nových telefónov ju už nemá a telefón musí byť na očiach |
| Nastavenie blesku pri notifikácii | Zadarmo | Funguje iba keď je telefón otočený, ruší okolie |

Light Potion zapĺňa medzeru: lacný, tichý a dekoratívny predmet, ktorý chráni súkromie.

## Funkčné požiadavky

| ID | Požiadavka | Zdroj |
|---|---|---|
| F1 | Aplikácia zachytí novú notifikáciu a zistí jej kategóriu | E1 |
| F2 | Aplikácia pošle do zariadenia cez Bluetooth LE 2 bajty: kategóriu a naliehavosť | E7, R8 |
| F3 | Zariadenie zobrazí farbu podľa kategórie: hovor zelená, správa modrá, e-mail žltá, iné biela | E1 |
| F4 | Svetlo bliká asi 1,8 s a zhasne za asi 0,7 s. Naliehavá notifikácia trvá asi 3 s a svieti naplno. | E1, R5 |
| F5 | Aplikácia sa sama znovu pripojí, keď sa zariadenie vráti do dosahu | E2 |
| F6 | Aplikácia ignoruje trvalé notifikácie, súhrny skupín a vlastné notifikácie | E1 |
| F7 | Aplikácia má testovacie tlačidlá pre všetky štyri kategórie | test |
| F8 | Neplatná správa (zlá dĺžka alebo hodnota) zariadenie nezhodí | spoľahlivosť |

## Nefunkčné požiadavky

| ID | Požiadavka | Cieľ |
|---|---|---|
| N1 | Oneskorenie od notifikácie po svetlo | do 2 s (E2) |
| N2 | Výdrž batérie (finálna verzia) | aspoň 7 dní (E3) |
| N3 | Rozmer | fľaštička široká asi 35 mm (E4) |
| N4 | Súkromie | text, nadpis ani odosielateľ nikdy neopustia telefón, ani v logoch. Aplikácia bez povolenia na internet. |
| N5 | Kompatibilita | Android 8.0 (API 26) a novší |
| N6 | Jas | normálna notifikácia obmedzená na asi 80 z 255, aby neoslňovala |

## Obmedzenia

- Android obmedzuje aplikácie na pozadí, preto je potrebná služba v popredí (RK1).
- Prístup k notifikáciám musí používateľ povoliť ručne v nastaveniach systému.
- Vo fľaštičke je veľmi málo miesta pre batériu a dosku (RK3).
- Prvá verzia bez párovania a šifrovania Bluetooth, keďže sa posielajú iba 2 bajty bez osobných údajov.

## Sekcie

- [Resources](./01.Resources/index.md) – súčiastky, knižnice a nástroje

---
**Navigation:** [⬆️ Up](../index.md) · [🏠 Home](../index.md)
