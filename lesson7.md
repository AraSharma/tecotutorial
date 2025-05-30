7.MATURITNÍ OTÁZKA

Zadání: TECO, praktická konfigurace ovladačů pomocí grafického jazyka CFC. Možnosti ovládání chytrého domu, vzdálené ovládání, nouzové ovládání na PLC. Připojení rozšiřujících modulů na sběrnici CIB. 

Úkol č.1: Po stisknutí levé horní části tlačítka na druhém ovladači (Logus) se rozsvítí halogenová žárovka. Zhasne podržením levého spodního tlačítka na druhém ovladači (Logus). 

Vpravo nahoře si otevřeme knihovny a stáhneme knihovnu iControlLib

Otevřeme funkční bloky knihovny a použijeme iDimmer, pojmenujeme tak ať jde poznat co programujeme

Dolů do setLevel dáme vstupní hodnotu 100 v REAL

Do LightON zapojíme druhé tlačítko Logus r8_p3_IN.DI.UP1

Do LightOFF zapojíme Logus r8_p3_IN.DI.PRESS_DOWN1

Do výstupu out zapojíme žárovku C-OR-0202B -> konkrétně r8_p4_OUT.DOs.DO1

Zkontrolujeme a máme hotovo!


<img width="697" alt="Snímek obrazovky 2568-05-28 v 18 05 00" src="https://github.com/user-attachments/assets/868aac91-2840-4cbc-bfb7-144a613f3336" />




Úkol č.2: Jakými dalšími způsoby lze ovládat chytrý dům, jaké rozšiřující moduly připojujeme k PLC a proč? Co je to CIB sběrnice?

Jakými dalšími způsoby lze ovládat chytrý dům?

Mobilní aplikace / webové rozhraní
→ Uživatel ovládá dům odkudkoli přes internet (např. přes Teco Webmaker nebo mobilní appku).

Hlasové ovládání (např. Google Assistant, Alexa)
→ Ovládání světel, teploty nebo žaluzií hlasem – pohodlné a moderní.

Pohybová čidla / přítomnost osob
→ Automatické spínání osvětlení nebo vytápění podle pohybu nebo obsazenosti místnosti.

Časové programy a scénáře
→ Ovládání zařízení podle nastaveného času (např. „večerní režim“, „odchod z domu“).

Nouzová tlačítka / lokální vstupy na PLC
→ Možnost ovládání i při výpadku komunikace nebo internetu – přímý zásah do řízení přes fyzické tlačítko.

Jaké rozšiřující moduly připojujeme k PLC a proč?

Vstupní a výstupní moduly (např. DI, DO, AI, AO)
→ Slouží k připojení více čidel, tlačítek, spínačů nebo k řízení dalších výstupů (světla, ventilátory atd.).

Moduly pro měření (např. teploty, CO₂, vlhkosti)
→ Umožňují monitorovat prostředí a automaticky řídit větrání, topení nebo klimatizaci.

RF moduly nebo bezdrátové brány
→ Slouží k propojení s bezdrátovými čidly nebo ovladači (např. pohybová čidla v místech bez kabeláže).

Energetické moduly (např. elektroměry, měření proudu, napětí)
→ Sledují spotřebu a pomáhají optimalizovat provoz a šetřit energii.

Záložní bateriové moduly nebo UPS
→ Zajišťují provoz systému i při výpadku napájení – důležité pro bezpečnostní a nouzové systémy.

Co je to CIB sběrnice?

CIB (Common Installation Bus)
→ Komunikační sběrnice vyvinutá firmou TECO pro snadné propojení periferních zařízení s PLC.

Přenáší data i napájení současně
→ Pomocí dvouvodičového kabelu zajišťuje jak komunikaci, tak napájení senzorů a ovladačů.

Jednoduchá instalace a rozšiřování
→ Vhodná pro inteligentní elektroinstalace, kde je potřeba propojit mnoho tlačítek, čidel nebo relé bez složité kabeláže.

Podpora více typů zařízení
→ Připojují se např. čidla pohybu, tlačítka Logus, LED ovladače, termostaty, reléové výstupy a další moduly.





