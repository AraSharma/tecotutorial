
# ⚡ 06 - Konfigurace elektroměru TECO & analog vs digitální signály

## 🎯 Zadání

**Úkol č. 1:**  
Nakonfigurujte elektroměr a zobrazte spotřebu na webu pomocí Webmakeru. Stránku graficky upravte.

## 🛠️ Postup

1. Stáhněte knihovnu `EnergyLib`, vložte blok `fbElectricityMeterPulse`.
2. Připojte `DI1` z C-HM-0308M do `Pulse` vstupu.
3. Přidejte vstupy:
   - `Voltage` (REAL) → 230 V
   - `Pulse_per_kWh` (UDINT) → 1000
   - `Counter` (UDINT)
4. Výstup `PowerUsage` (REAL) zobrazte přes Webmaker.
5. Přidejte pole pro výpis výstupní hodnoty.

## 💡 Úkol č. 2

**Proč měřit spotřebu?**
- Přehled a optimalizace nákladů
- Odhalení poruch a neefektivity
- Ekologické uvědomění

**Co měřit?**
- Celkovou spotřebu, spotřebu zařízení, napětí, proud, výkon

**Analog vs Digitální signál:**

| Vlastnost        | Analogový signál     | Digitální signál        |
|------------------|----------------------|--------------------------|
| Povaha           | Spojitý              | Diskrétní (0/1)          |
| Přesnost         | Méně přesný          | Vyšší přesnost           |
| Použití          | Teplota, tlak        | Tlačítka, spínače        |
| Odolnost vůči rušení | Nižší            | Vysoká                   |
    