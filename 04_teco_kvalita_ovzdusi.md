
# 🌬️ 04 - Snímání kvality ovzduší & automatická ventilace (TECO)

## 🎯 Zadání

**Úkol č. 1:**  
Nastavte topnou hlavici a ventilátor, aby se zapnuly při poklesu teploty pod 20 °C. Zobrazte aktuální teplotu na displeji.

## 🛠️ Postup

1. Vložte blok `Greater Than` a porovnejte teplotu s 20 °C.
2. Výsledek (BOOL) převeďte přes `INT` a `MUL` na hodnotu 100.
3. Převeďte `INT` na `REAL` a propojte s topnou hlavicí (100%) a ventilátorem (zapnutí).
4. Zobrazte teplotu pomocí převodu z `REAL` na `INT`, násobení 10 a propojení na displej.

## 💡 Úkol č. 2

**Rozdíly:**
- Větrání = přirozené, manuální
- Ventilace = řízená, často se senzory
- Klimatizace = teplota + vlhkost, filtrace

**Výhody automatického řízení:**
- Úspora energie, reakce na aktuální potřebu
- Napojení na časové režimy nebo přítomnost osob

**Sledované parametry:**
- Teplota, vlhkost, CO₂, TVOC, prachové částice (PM), zápachy

**Typické látky:**
- CO₂ (ppm), TVOC (ppb/mg/m³), PM2.5/PM10, vlhkost (%), teplota (°C)
    