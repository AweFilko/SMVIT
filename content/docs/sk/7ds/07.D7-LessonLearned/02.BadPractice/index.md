# Bad Practice

- **Dva názvy projektu.** Časť súborov používala „Potion Notifier“, časť „Light Potion“. Názov treba zjednotiť hneď na začiatku.
- **Úpravy dokumentácie v priečinku, ktorý build prepisuje.** Dokumentácia sa upravovala priamo v `publishing/docusaurus/docs`, ktorý príkaz `make build` prepíše obsahom z `content/docs`. Hrozí strata práce.
- **Pôvodný míľnik M5 počítal s MOSFETom na nepájivom poli.** Rozsah prototypu sa zmenil až neskôr. Rozsah prototypu treba stanoviť pred plánovaním míľnikov.
- **Nezapisovaný čas a ceny.** Hodiny a ceny súčiastok sa nezapisovali priebežne, teraz sa musia dopĺňať spätne.
- **Výsledky testov až na konci.** Výsledky ručných testov sa majú zapisovať do D6 hneď po teste.

---
**Navigation:** [⬆️ Up](../index.md) · [🏠 Home](../../index.md)
