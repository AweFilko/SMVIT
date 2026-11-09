# Strategy

## Prístup

1. **Hardvér držať jednoduchý.** Použiť dosku Seeed XIAO ESP32-C3, ktorá už má nabíjačku LiPo článku a regulátor 3,3 V. Bez samostatnej nabíjacej dosky.
2. **Najprv Android.** Android umožňuje aplikácii čítať notifikácie. Aplikácia pošle zariadeniu kategóriu, vďaka čomu je firmvér jednoduchý.
3. **Súkromie už v návrhu.** Cez Bluetooth sa posiela iba kategória a naliehavosť, nikdy text správy.
4. **Nízka spotreba.** Dlhý interval Bluetooth spojenia, napájanie LED sa v pokoji vypína cez MOSFET, jas je obmedzený.
5. **Urobiť z toho pekný predmet.** Vzhľad starej fľaštičky s korkovým viečkom a mosadznou objímkou, nie obyčajná plastová krabička.
6. **Nakupovať v EÚ.** Objednávať v obchodoch v EÚ (napríklad Botland), aby sa na Slovensku neplatilo clo.

## Riziká

| Riziko | Opatrenie |
|---|---|
| Android zastaví aplikáciu na pozadí | Služba v popredí, výnimka z optimalizácie batérie, test na dvoch značkách telefónov |
| Pokojový prúd je vyšší, než odhad | Merať včas, upraviť interval spojenia |
| Batéria je pre fľaštičku príliš veľká | Zvolený článok 250 mAh, pred objednávkou overiť rozmery |
| Bezpečnosť LiPo | Chránený článok, kontrola polarity, nezvierať v puzdre |

---
**Navigation:** [⬆️ Up](../index.md) · [🏠 Home](../../index.md)
