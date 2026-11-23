# Publishing

## Kde sa projekt nachádza

| Čo | Kde |
|---|---|
| Dokumentácia 7Ds | Tento web (Docusaurus), sekcia 7Ds |
| Zdrojový kód firmvéru a aplikácie | [github.com/AweFilko/LightPotion](https://github.com/AweFilko/LightPotion) |
| Ukážková webová stránka | [Website v0.2](pathname:///knifes_overview/assets/Light_Potion_v0.2.html) |
| 3D model | [3D model](pathname:///knifes_overview/assets/Potion_Notifier_3D_model.html) |

## Ako spustiť dokumentáciu lokálne

V priečinku `publishing/docusaurus`:

```sh
npm install      # iba prvýkrát
npm run start    # dev server na http://localhost:3000
```

## Pravidlá publikovania

- Dokumentácia je v slovenčine, kód a jeho komentáre v angličtine.
- Fotky sú uložené priamo pri stránke, ktorá ich používa (napríklad `05.D5-Implementation/img/`).
- HTML stránky (web, 3D model) sú v `static/assets`.
- Text notifikácií ani osobné údaje sa nikdy nezverejňujú, ani v ukážkach logov.

## Plánované

- Zverejniť skompilované APK aplikácie ako vydanie (release) na GitHube po dokončení testov.
- Doplniť video z ukážky (míľnik M10).

---
**Navigation:** [⬆️ Up](../index.md) · [🏠 Home](../../index.md)
