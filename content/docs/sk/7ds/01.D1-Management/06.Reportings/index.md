# Reportings

## Správa o stave – 2026-11-23

**Celkový stav:** prototyp na nepájivom poli je hotový, otestovaný a funguje. Telefón s aplikáciou zachytí skutočnú notifikáciu a zariadenie zasvieti správnou farbou. Ďalšia fáza je finálna verzia s batériou vo fľaštičke.

### Hotovo

- Koncept, ciele, stratégia, rozhodnutia a riziká (D1)
- 3D model, schéma zapojenia a ukážková webová stránka
- Prototyp: ESP32-C3 Super Mini a modul WS2812 na nepájivom poli, napájanie z USB-C
- Firmvér v0.1.0: Bluetooth LE služba a animácia „blikanie a zhasnutie“
- Aplikácia pre Android v0.1.0: nastavenie povolení, pripojenie, služba v popredí, čítanie notifikácií, testovacie tlačidlá
- Jednotkové testy mapovania kategórií, všetky prešli
- Testy firmvéru T1–T10 a aplikácie A1–A12, všetky prešli (pozri [D6](../../06.D6-Verification-Testing/index.md))

### Ďalšie kroky

- Objednať súčiastky pre finálnu verziu (XIAO ESP32-C3, LiPo 250 mAh, MOSFETy, tlačidlo)
- Upraviť firmvér pre finálnu dosku
- Vytlačiť fľaštičku a zložiť zariadenie
- Zmerať pokojový prúd a výdrž batérie

### Riziká a problémy

- RK1 (Android zastaví aplikáciu na pozadí): na testovacom telefóne sa neprejavilo, aplikácia reagovala aj po zatvorení zo zoznamu posledných (test A10). Test na druhej značke telefónu (opatrenie M1) ešte ostáva.

## Ďalšie správy

Ďalšia správa sa doplní po zložení finálnej verzie.

---
**Navigation:** [⬆️ Up](../index.md) · [🏠 Home](../../index.md)
