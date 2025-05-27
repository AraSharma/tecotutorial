# 💡 TECO – Praktická konfigurace uživatelského rozhraní pomocí WebMakeru (Mosaic)

Tento návod popisuje základní konfiguraci ovládacího webového rozhraní v prostředí **Mosaic** pomocí integrovaného nástroje **WebMaker**. Cílem je vytvořit funkční ovládání halogenové žárovky pomocí webového rozhraní a pochopit přínosy webových UI v systému chytré domácnosti.

---

## ✅ Úkol č. 1 – Ovládání žárovky přes webové rozhraní

### 🎯 Zadání

- Po stisknutí **prvního tlačítka** na webovém rozhraní se **rozsvítí halogenová žárovka**.
- Po stisknutí **druhého tlačítka** žárovka **zhasne**.
- Přidáme i **třetí tlačítko**, které umožní **zapnutí i vypnutí současně** (kombinovaná akce).

---

### 🛠️ Postup

#### 1. Instalace knihovny

- Klikneme na **ikonu knihovny** v levém horním rohu (pod logem Mosaic).
- Nainstalujeme knihovnu: **`iControlLib`**.

#### 2. Vytvoření tabulky `fb_DimmerLED`

- Vytvoříme tabulku `fb_DimmerLED`.
- Přidáme blok `set level` (např. proměnná `bcfgs`) s inicializací na **100**.
- V PLC vpravo najdeme modul **C-OR-0202B**.
  - Použijeme výstup **R8 - P4 - OUT**.
  - Zapojíme přes **DO1 → OUT**.

> 🖼️ *Obrázek 1: Ukázka tabulky (fb_DimmerLED)*  
> *(Zde můžeš vložit odkaz na obrázek po jeho nahrání do repozitáře: `![Popis](obrazky/tabulka-fb_DimmerLED.png)`)*

#### 3. Aktivace WebMakeru

- Klikneme na ikonu **WebMaker** v horní liště.

> 🖼️ *Obrázek 2: Otevření WebMakeru*

#### 4. Přidání tlačítek

- Přidáme **první tlačítko** – pojmenujeme ho např. `Zapnout`, přiřadíme proměnnou pro zapnutí.
- Přidáme **druhé tlačítko** – `Vypnout`, přiřadíme proměnnou pro vypnutí.
- Přidáme **třetí tlačítko** – `Přepnout`, které ovládá obě akce.

> 🖼️ *Obrázek 3: Přidání tlačítek*  
> 🖼️ *Obrázek 4: Nastavení proměnných k tlačítkům*

#### 5. Dokončení

- Klikneme na **OK**.
- Nahrajeme projekt do PLC.
- Spustíme.

---

## 💭 Úkol č. 2 – Proč je výhodné webové rozhraní pro chytrý dům?

Vytvoření webového rozhraní pro chytrý dům přináší **řadu výhod z hlediska uživatelského komfortu i technické správy**:

### ⚙️ Výhody webového rozhraní

- **Snadná dostupnost** – přístup přes běžný prohlížeč z jakéhokoli zařízení bez potřeby instalace aplikací.
- **Centralizace ovládání** – všechna zařízení lze ovládat z jednoho místa.
- **Uživatelská přívětivost** – design lze snadno přizpůsobit různým uživatelům.
- **Vzdálený přístup** – možnost monitoringu a řízení mimo domov.
- **Flexibilita a rozšiřitelnost** – snadné doplnění nových funkcí.

---

## 📎 Soubory ke stažení

| Soubor              | Popis                          |
|---------------------|-------------------------------|
| `program.iec`       | IEC program pro Mosaic         |
| `fb_DimmerLED.tab`  | Tabulka s konfigurací          |
| `webmaker.ui`       | Projekt webového rozhraní      |
| `obrazky/`          | Složka s doprovodnými obrázky  |

> *(Tyto soubory nahraj do stejného repozitáře, případně vytvoř složky.)*

---

## 📌 Poznámka

Tento návod slouží jako úvodní ukázka praktického využití WebMakeru v systému TECO. Pro složitější aplikace doporučujeme zabezpečení přístupu, pokročilé dynamické prvky a testování na více zařízeních.

---

## 📧 Kontakt / Autor

Připravil: *[Tvoje jméno nebo přezdívka]*  
Repozitář: [github.com/tvoje-uzivatelske-jmeno/teco-navody](https://github.com/tvoje-uzivatelske-jmeno/teco-navody)
