
# 🧪 02 - Konfigurace relé modulů (TECO) & technologie spínání

## 🎯 Zadání

**Úkol č. 1:**  
Po stisknutí levého horního tlačítka na ovladači typu Logus (`r8_p2_IN.DI.UP1`) se rozsvítí horizontální LED pásek a zapne ventilátor.  
Po 7 sekundách se obě zařízení automaticky vypnou.

**Úkol č. 2:**  
Jaké existují technologie spínání? Popiš jejich princip a možné využití relé modulů.

---

## 🛠️ Řešení úkolu č. 1 (v Mosaic)

1. Pokud ještě nemáš, nainstaluj knihovnu `iDimmer`.
2. Použij programovací blok `iDimmerLED` a pojmenuj ho dle zvyklostí.
3. Nastav jednotlivé vstupy a výstupy podle následujícího schématu:

<img width="522" alt="o2o1" src="https://github.com/user-attachments/assets/e3d226d1-0497-4676-8797-997fbeebdc3a" />

---

## 💡 Úkol č. 2 - Technologie spínání

Mezi běžné technologie spínání patří:

- **Mechanické relé** – Spínání pomocí elektromagnetu, mechanický pohyb kontaktu.
- **Polovodičové relé (SSR)** – Spínání bez pohyblivých částí, rychlé a bezhlučné.
- **Triak / Tyristor** – Používají se pro AC spínání, často u stmívačů.
- **MOSFET / IGBT** – Spínání DC zátěží, rychlé, účinné, často ve výkonové elektronice.

### 🎯 Možné využití relé modulů

- Ovládání světel, ventilátorů, topení
- Přepínání režimů zařízení
- Oddělení řídicí logiky od silových obvodů
