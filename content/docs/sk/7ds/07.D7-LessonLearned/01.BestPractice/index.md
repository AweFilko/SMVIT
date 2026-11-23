# Best Practice

- **Najprv prototyp bez batérie.** Doska napájaná z USB a jeden modul LED stačili na overenie celej cesty od notifikácie po svetlo. Batéria a MOSFETy by ladenie zbytočne skomplikovali.
- **Jedna dohoda o protokole.** UUID a formát 2 bajtov sú rovnako v `config.h` aj v `BleContract.kt`. Obe strany sa dali písať nezávisle.
- **Testovať firmvér bez aplikácie.** Aplikácia nRF Connect umožní zapísať bajty priamo, takže chyba sa dá rýchlo nájsť buď vo firmvéri, alebo v aplikácii.
- **Všetky nastavenia v `config.h`.** Pin, počet LED, jas a časy sa menia na jednom mieste. Prechod na dosku XIAO bude jednoduchý.
- **Neblokujúca animácia.** Animácia cez `millis()` namiesto `delay()` neblokuje Bluetooth, takže nová notifikácia môže prísť kedykoľvek.
- **Súkromie už v návrhu.** Telefón posiela iba kategóriu a aplikácia nemá povolenie na internet. Netreba riešiť ochranu osobných údajov v zariadení.
- **Rozdelenie práce podľa rozhrania.** Filip robil hardvér a firmvér, Lucia aplikáciu. Keďže protokol bol dohodnutý vopred, nikto nemusel čakať na druhého.
- **Písomné technické zadanie.** Súbor `CLAUDE.md` s hardvérom, protokolom, pravidlami a kritériami prijatia držal obe časti v súlade a slúžil aj ako podklad pre návody na testovanie.
- **Malé commity.** Každý krok (firmvér, návod, aplikácia, testy) má vlastný commit.
- **Rozhodnutia s ID.** Pravidlá R1–R9 odkazujú na rozhodnutia D-001 až D-008, takže je jasné, prečo je niečo tak.

---
**Navigation:** [⬆️ Up](../index.md) · [🏠 Home](../../index.md)
