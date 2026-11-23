# Troubleshooting

| Problém | Možná príčina | Riešenie |
|---|---|---|
| Počítač dosku nevidí, nahratie zlyhá | Kábel iba na nabíjanie | Použiť dátový kábel USB-C. Prípadne pri pripájaní podržať tlačidlo BOOT. |
| Sériový výpis je prázdny | Chýba USB CDC | V `platformio.ini` musia byť `ARDUINO_USB_MODE=1` a `ARDUINO_USB_CDC_ON_BOOT=1` |
| LED vôbec nesvieti | Zlý pin alebo zapojenie | Overiť DI na GPIO4, GND na G, napájanie na 3V3. Skontrolovať spoje po spájkovaní. |
| LED bliká náhodne alebo má zlé farby | 3,3 V nestačí na dátový signál | Napájanie LED presunúť na 5V, do dátového vodiča dať 330 Ω |
| Doska po zapojení LED neštartuje | LED na GPIO2, GPIO8 alebo GPIO9 | Použiť GPIO4 |
| Zariadenie sa v nRF Connect nezobrazí s názvom | Názov je až v odpovedi na skenovanie | Hľadať podľa UUID služby `4c50ff00-…` |
| Zápis nič nespraví, vo výpise `WARN bad payload` | Zlá dĺžka alebo hodnota | Posielať presne 2 bajty, kategória 0–3, naliehavosť 0–1 |
| Aplikácia ostáva v stave „Scanning“ | Chýba povolenie, Bluetooth je vypnutý alebo doska je mimo dosahu | Skontrolovať zoznam povolení, zapnúť Bluetooth, priblížiť dosku |
| Chyba GATT 133 pri pripojení | Známa chyba Androidu | Aplikácia to sama skúsi znova. Pomôže aj vypnúť a zapnúť Bluetooth. |
| LED reaguje na testovacie tlačidlá, ale nie na notifikácie | Prístup k notifikáciám nie je povolený | Nastavenia → Prístup k notifikáciám → zapnúť Light Potion |
| Po čase notifikácie prestanú chodiť | Android zastavil aplikáciu na pozadí | Povoliť výnimku z optimalizácie batérie, pri niektorých značkách aj automatické spúšťanie |
| E-mail svieti bielo namiesto žltej | Aplikácia nenastavila kategóriu notifikácie | Zatiaľ bez riešenia, pozri otázku Q5 a návrh P1 |

Problémy finálnej verzie (batéria, MOSFET, nabíjanie) sa doplnia po jej zložení.

---
**Navigation:** [⬆️ Up](../index.md) · [🏠 Home](../../index.md)
