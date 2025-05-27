
# ⚡ 06 - Konfigurace elektroměru TECO & analog vs digitální signály

## 🎯 Zadání

**Úkol č. 1:**  
Nakonfigurujte elektroměr a zobrazte spotřebu na webu pomocí Webmakeru. Stránku graficky upravte.

## 🛠️ Postup

1. Stáhněte knihovnu `EnergyLib`, vložte blok `fbElectricityMeterPulse`.
2. Připojte `DI1` z C-HM-0308M do `Pulse` vstupu.
3. Přidejte vstupy:
   - `Voltage` (REAL) → 230
   - `Pulse_per_kWh` (UDINT) → 1000
   - `Counter` (UDINT)
4. Výstup `PowerUsage` (REAL) zobrazte přes Webmaker.
5. Přidejte pole pro výpis výstupní hodnoty.
<img width="559" alt="Snímek obrazovky 2568-05-28 v 0 12 37" src="https://github.com/user-attachments/assets/9be28cca-c868-4e7d-b2bd-5ba8bf74bc0e" />

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
    
