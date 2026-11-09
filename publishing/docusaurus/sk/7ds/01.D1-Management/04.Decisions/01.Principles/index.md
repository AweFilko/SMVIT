# Principles

Princípy, ktorými sa riadia všetky rozhodnutia v projekte Potion Notifier.

| # | Princíp | Čo to znamená v praxi |
|---|---|---|
| 1 | Jednoduchosť | Radšej menej súčiastok. Doska XIAO ESP32-C3 už obsahuje nabíjačku, takže bez TP4056. |
| 2 | Súkromie na prvom mieste | Cez Bluetooth sa posiela iba kategória a naliehavosť, nikdy text správy. |
| 3 | Nízka spotreba | Napájanie LED sa v pokoji vypína a jas je obmedzený. |
| 4 | Bezpečnosť batérie | Iba chránený LiPo článok a kontrola polarity pred pripojením. |
| 5 | Jedna platforma naraz | Najprv Android, iPhone až neskôr. |
| 6 | Predmet, nie len gadget | Vzhľad starej fľaštičky s korkovým viečkom a mosadznou objímkou. |
| 7 | Merať, nie hádať | Odhady (výdrž asi 8 dní, pokojový prúd asi 1 mA) sa overia meraním. |

---
**Navigation:** [⬆️ Up](../index.md) · [🏠 Home](../../../index.md)
