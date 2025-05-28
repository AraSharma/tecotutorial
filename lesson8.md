
Zadání: 8. TECO, monitorování stavu ovzduší a ventilace, praktické programování v jazyce CFC. Snímání dat ze senzorů kouře a kvality ovzduší, automatické spouštění odvětrávání, tvorba grafického uživatelského rozhraní. 

Úkol č.1: Za pomocí knihovny iFan a porovnávacích knihoven (např. GT, nebo GE) nastavte požadovanou hodnotu teploty v místnosti a porovnejte s aktuálně měřenou pomocí topné hlavice. Pokud je měřená teplota vyšší, než nastavená, spusťte ventilátor. V opačném případě se ventilátor vypne, nebo se vůbec nespustí. Po celou dobu bude měřená teplota vypsaná na displeji. 

1.klikni na průzkumník knihoven (knihy s lupou ikona) 

2.přidej knihovnu iControlLib_V35_20230620 (knihy s plusem ikona) 

3.z knihovny iControlLib_V35_20230620 vyber funkční blok fb_iFan a přidej ho 

4.pojmenuj iFan funkční blok dle své preference 

5.přidej proměnou kteá má kontext VAR_GLOBAL_RETAIN a nastav hodnou 100 (typ proměnné je REAL) 

6.Připoj proměnou do setLevel 

7.V postranním panelu aktuální konfigurace v záložce Interní Sběrnice najdi zařízení (v naší konfiguraci to najdete C-HC-0201F-E), které obsahuje poloku iTherm a přetáhni ji do prostředí 

8.Vytvoř proměnnou, která je kontextem VAR a typem REAL a nastav hodnotu na požadovanou teplotu 

9.Vložíme blok ze zelné ikony (vložit POU) a vybereme ze záložky relační blok GT 

10.Do horního vstupu bloku GT připojíme položku ITHERM a do spodního vstupu proměnnou s požadovanou teplotou (bod 8) 

11.Výstup bloku GT zapojíme do IFAN vstupu fanOn 

12.Vložíme blok ze zelné ikony (vložit POU) a vybereme ze záložky logické blok NOT 

13.Výstup blok NOT zapoj do IFAN položky fanOff a vstup zapojíme opět do výstupu bloku GT 

14.V postranním panelu aktuální konfigurace v záložce Interní Sběrnice najdi zařízení (v naší konfiguraci to najdete C-HM-0308M), které obsahuje poloku DO1 (pro zapnutí ventilátoru) a přetáhni ji do prostředí 

15.Výstup out z bloku iFan zapoj do této položky (bod 14) 



 

Přidání displaye: 

16.V postranním panelu aktuální konfigurace v záložce Interní Sběrnice najdi zařízení (v naší konfiguraci to najdete C-RC-0003R), které obsahuje položku VAL1 (pro zobrazení hodnoty displaye) a přetáhni ji do prostředí 

17.Vložíme blok ze zelené ikony (vložit POU) a vybereme ze záložky konverzní blok REAL_TO_INT 

18.Do vstupu zapojíme položku ITHERM (bod 7) avýstup zapojíme do položky displaye (bod 16) 

  <img width="670" alt="Snímek obrazovky 2568-05-28 v 11 06 53" src="https://github.com/user-attachments/assets/38416629-12b1-404e-a80d-55839299df68" />


Máme hotovo! 



Úkol č.2: Jaké další parametry ovzduší monitorujeme a proč?

Co všechno sledujeme na kvalitě ovzduší

Teplota – komfortní pobyt, řízení topení/chlazení.

Vlhkost – prevence proti plísním (nízká vlhkost dráždí sliznice, vysoká podporuje růst plísní).

CO₂ koncentrace – ukazatel vydýchaného vzduchu, důležité pro pozornost a zdraví.

Těkavé organické látky (TVOC) – např. z nábytku, čistících prostředků – škodlivé pro zdraví.

Prachové částice (PM2.5 / PM10) – vliv na dýchací systém.

Zápachy / kvalita vzduchu obecně (pachové senzory).



