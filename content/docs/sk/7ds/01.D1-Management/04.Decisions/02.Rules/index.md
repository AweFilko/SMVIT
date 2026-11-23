# Rules

Konkrétne pravidlá odvodené z rozhodnutí. Všetky boli schválené 2026-11-03.

| ID | Pravidlo | Dôvod | Rozhodnutie |
|---|---|---|---|
| R1 | Používame dosku XIAO ESP32-C3. Samostatnú nabíjačku TP4056 nepoužívame. | Doska už batériu nabíja, druhá nabíjačka by bola zbytočná. | D-001 |
| R2 | Prvou platformou je Android. | Telefón vlastníka. Android potrebuje sprievodnú aplikáciu, iPhone príde neskôr. | D-002 |
| R3 | Batéria je chránený LiPo článok 250 mAh. | 1000 mAh je na kľúčenku príliš veľký, asi 8 dní stačí. | D-003 |
| R4 | Jedno tlačidlo s aretáciou na korkovom viečku zapína a vypína batériu. Iné tlačidlá nepoužívame. | Nahrádza posuvný spínač aj samostatné používateľské tlačidlo. | D-004 |
| R5 | Svetlo bliká 2–3 s a samo zhasne. Zrušenie svetla nie je. | Jednoduchšie zariadenie bez vstupu. | D-005 |
| R6 | LED sa napájajú cez P-MOSFET Q2, ktorý riadi N-MOSFET Q1. | GPIO s 3,3 V nevie priamo spínať P-MOSFET so zdrojom na 4,2 V. | D-006 |
| R7 | Puzdro má tvar fľaštičky a port USB-C je na spodku. | Inšpirácia starými fľaštičkami s elixírom. | D-007 |
| R8 | Cez Bluetooth sa posiela iba kategória a naliehavosť. | Súkromie a jednoduchý formát správy. | D-008 |
| R9 | Firmvér nastaví dátový pin LED (GPIO4) na nízku úroveň pred vypnutím napájania LED. | Dátový vstup by inak mohol cez ochrannú diódu napájať LED späť. | Schéma zapojenia |

---
**Navigation:** [⬆️ Up](../index.md) · [🏠 Home](../../../index.md)
