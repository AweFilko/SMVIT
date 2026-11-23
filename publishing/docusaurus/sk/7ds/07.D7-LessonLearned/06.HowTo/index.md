# How To

## Nahrať firmvér do dosky

1. Pripojiť ESP32-C3 káblom USB-C, ktorý prenáša dáta (nie iba nabíjací).
2. V priečinku `firmware` spustiť `pio run -t upload`.
3. Spustiť `pio device monitor` a overiť výpis `LightPotion fw 0.1.0` a `BLE advertising`.

## Otestovať zariadenie bez aplikácie

1. Nainštalovať nRF Connect for Mobile (Nordic Semiconductor).
2. V záložke Scanner nájsť zariadenie **LightPotion** a pripojiť sa.
3. Otvoriť službu `4c50ff00-…`, pri charakteristike `4c50ff01-…` stlačiť šípku hore.
4. Zvoliť BYTE ARRAY, zadať `0200` a odoslať. LED blikne modro.

## Nainštalovať a nastaviť aplikáciu

1. V priečinku `android` spustiť `./gradlew assembleDebug`.
2. Nainštalovať: `adb install app/build/outputs/apk/debug/app-debug.apk`
3. V aplikácii udeliť povolenia zo zoznamu, prístup k notifikáciám zapnúť v nastaveniach systému.
4. Počkať na stav **Connected** a vyskúšať testovacie tlačidlá.

## Zmeniť pin alebo počet LED

V `firmware/include/config.h` upraviť `LED_PIN` alebo `NUM_LEDS` a firmvér znova nahrať. Na LED nepoužívať GPIO2, GPIO8 ani GPIO9.

## Spustiť túto dokumentáciu

V `publishing/docusaurus` spustiť `npm run start` a otvoriť `http://localhost:3000`.

---
**Navigation:** [⬆️ Up](../index.md) · [🏠 Home](../../index.md)
