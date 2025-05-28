Zadání: TECO, praktické programování v jazyce CFC. Odpadové hospodářství a vytápění. Snímání dat z vodoměru a topné hlavy. Nastavení vytápění. 

Úkol č.1: Za pomocí knihovny iFan a porovnávacích knihoven (např. GT, nebo GE) nastavte požadovanou hodnotu teploty v místnosti a porovnejte s aktuálně měřenou pomocí topné hlavice. Pokud je měřená teplota nižší, než nastavená, otevřete ventil v topné hlavici do stavu 100 (otevřena) v opačném případě topná hlava uzavře ventil do polohy 0 (zavřeno). 

Příprava mosaic: 

1.vytvořit novou skupinu projektů 

2.vytvořit nový projekt 

3.nastavit stejnou IP adresu na PC jako je v kufříku 

4.připojit se přes ethernet v Mosaicu 

5.Stáhnout konfiguraci kufříku (obrazek ozubene kolecko oranzova sipka) 

 

Implemntace funkčnosti: 

1.klikni na průzkumník knihoven (knihy s lupou ikona) 

2.přidej knihovnu iControlLib_V35_20230620 (knihy s plusem ikona) 

3.z knihovny iControlLib_V35_20230620 vyber funkční blok fb_iFan a přidej ho 

4.pojmenuj iFan funkční blok dle své preference 

5.přidej proměnou kteá má kontext VAR_GLOBAL_RETAIN a nastav hodnou 100 (typ proměnné je REAL) 

6.Připoj proměnou do setLevel 

7.V postranním panelu aktuální konfigurace v záložce Interní Sběrnice najdi zařízení (v naší konfiguraci to najdete C-HC-0201F-E), které obsahuje poloku iTherm a přetáhni ji do prostředí 

8.Vytvoř proměnnou, která je kontextem VAR a typem REAL a nastav hodnotu na požadovanou teplotu 

9.Vložíme blok ze zelné ikony (vložit POU) a vybereme ze záložky relační blok LT 

10.Do horního vstupu bloku LT připojíme položku ITHERM a do spodního vstupu proměnnou s požadovanou teplotou (bod 8) 

11.Výstup bloku LT zapojíme do IFAN vstupu fanOn 

12.Vložíme blok ze zelné ikony (vložit POU) a vybereme ze záložky logické blok NOT 

13.Výstup blok NOT zapoj do IFAN položky fanOff a vstup zapojíme opět do výstupu bloku LT 

14.V postranním panelu aktuální konfigurace v záložce Interní Sběrnice najdi zařízení (v naší konfiguraci to najdete C-HC-0201F-E), které obsahuje položku POSITION (pro nastavení pozice topné hlavice 0-100) a přetáhni ji do prostředí 

15.Výstup level z bloku iFan zapoj do této položky (bod 14) 

 <img width="713" alt="Snímek obrazovky 2568-05-28 v 11 11 04" src="https://github.com/user-attachments/assets/1bd98cb8-7fe0-4853-8b9d-882e61e670d9" />


Máme hotovo! 



Úkol č.2: Dle jaké měřené hodnoty poznáme, že probíhá odběr vody měřený vodoměrem? Co snímaná hodnota vyjadřuje?

Dle jaké měřené hodnoty poznáme, že probíhá odběr vody?

Počet impulzů z vodoměru (digitální vstup)
→ Moderní vodoměry vydávají impulzy (např. 1 impuls = 1 litr vody); pokud impulzy přibývají, probíhá odběr.

Rychlost změny impulzů / frekvence
→ Vyšší frekvence impulzů značí rychlejší průtok vody – tedy větší aktuální odběr.

Okamžitý průtok (pokud se počítá v PLC)
→ Z impulzů lze dopočítat aktuální průtok (např. litry za minutu), což přímo říká, že dochází k odběru.

Změna celkového objemu vody v čase
→ Pokud se hodnota objemu vody mění (např. v intervalu každých 5 vteřin), víme, že někdo právě vodu odebírá.

Co snímaná hodnota vyjadřuje?

Množství spotřebované vody (např. v litrech nebo m³)
→ Celkové číslo ukazuje, kolik vody proteklo přes vodoměr za sledované období.

Průtok (pokud se počítá z impulzů)
→ Udává, jak rychle voda aktuálně protéká potrubím – pomáhá detekovat úniky nebo zvýšenou spotřebu.

Časovou závislost spotřeby (např. v grafu)
→ Můžeme sledovat, kdy a v jakých časech se voda spotřebovává (např. denní nebo noční odběr).

Podklad pro fakturaci nebo optimalizaci provozu
→ Hodnoty lze využít pro vyúčtování nebo úsporu vody v domácnosti / budově.





