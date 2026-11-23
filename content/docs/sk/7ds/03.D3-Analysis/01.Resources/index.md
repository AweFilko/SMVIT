# Resources

Analýza technických zdrojov: z čoho sa zariadenie skladá a čím sa vyvíja. Ľudia, čas a financie sú v [D1 – Resources](../../01.D1-Management/08.Resources/index.md).

## Hardvér

| Zdroj | Prototyp | Finálna verzia | Prečo |
|---|---|---|---|
| Doska | ESP32-C3 Super Mini | Seeed XIAO ESP32-C3 | Bluetooth LE, malá, lacná. XIAO má nabíjačku LiPo a regulátor 3,3 V (R1). |
| LED | 1 modul WS2812 | 3 LED WS2812B | Jeden dátový vodič, ľubovoľná farba |
| Napájanie | USB-C z počítača | LiPo 250 mAh, nabíjanie cez USB-C | Prototyp nepotrebuje batériu |
| Spínanie LED | žiadne | MOSFETy Q1 2N7002 a Q2 AO3401 | V pokoji LED úplne vypnúť a ušetriť batériu (R6) |
| Vypínač | žiadny | tlačidlo s aretáciou v korkovom viečku | Úplné odpojenie batérie (R4) |
| Puzdro | nepájivé pole | 3D tlačená matná fľaštička | Vzhľad elixíru (R7) |

## Softvér a knižnice

| Zdroj | Verzia | Použitie |
|---|---|---|
| PlatformIO, platforma espressif32 | 8.0.0 | Kompilácia a nahrávanie firmvéru |
| Arduino framework | – | Základ firmvéru |
| NimBLE-Arduino | 2.5.2 | Bluetooth LE na doske (úspornejšie ako štandardná knižnica) |
| FastLED | 3.10.9 | Ovládanie LED WS2812 |
| Kotlin | 2.0.21 | Jazyk aplikácie |
| Jetpack Compose, Material 3 | BOM 2024.12.01 | Používateľské rozhranie |
| Android Gradle Plugin | 8.7.3 | Build aplikácie (compileSdk a targetSdk 35, minSdk 26) |
| Kotlin coroutines | 1.9.0 | Asynchrónna práca s Bluetooth |
| JUnit | 4.13.2 | Jednotkové testy |

Aplikácia nepoužíva žiadnu knižnicu tretej strany pre Bluetooth ani analytiku.

## Nástroje

| Nástroj | Použitie |
|---|---|
| IntelliJ IDEA / Android Studio | Vývoj aplikácie |
| nRF Connect for Mobile | Test firmvéru bez aplikácie |
| Spájkovačka, cín, multimeter | Zapojenie a meranie |
| 3D tlačiareň | Fľaštička (plánované) |
| Claude Code (AI asistent) | Pomocný nástroj pri programovaní a písaní dokumentácie |

---
**Navigation:** [⬆️ Up](../index.md) · [🏠 Home](../../index.md)
