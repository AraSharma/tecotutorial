
# Maturitní příprava: Node-RED a Mosaic

## Node-RED

### 17. Maturitní otázka
17.MATURITNÍ OTÁZKA
Zadání: 17. Praktické cvičení v programu Node-Red – práce s API, přístupový token, zpracování dat pomocí funkce, výpis dat. Teorie způsobu zápisu dat JSON, porovnání s XML. 
Nastavte datovou sadu na webové https://api.golemio.cz/v2/pid/docs/openapi/ tak, aby do vašeho řešení v programu Node-red přicházela data o aktuální pozici všech autobusů na lince 176 a jejich aktuální odchylce od jízdního řádu. Poté se pokuste vypsat do debugu průměrnou hodnotu odchylky všech autobusů na lince 176 v danou chvíli. Autorizační klíč máte k dispozici na ploše počítače v textovém souboru.
Připravím si blok inject/timestamp, který následně „vysílá“ signál a spouští reakce.
Následně si připravím blok http request, který následně získává data z golemia. Blok vyšle „poptávku“ do golemia a čeká na odpověď.
Otevřu si stránku api.golemio -> public vehicle positions -> přihlásím se pomocí x-access-tokenu, který najdu na ploše v poznámkovém bloku
Kliknu na try-it-out a změním předvyplněný údaj (číslo autobusu a transport type) na linku 176 a bus. Nic jiného neměním. 

Kliknu na execute a zkopíruji odkaz

Odkaz vložím do bloku http request do řádku URL





Ve stejném bloku o kus níže založím nový header a v kolonce nad změním na JSON object. Do prvního pole headers zadám X-Access-Token a do druhého pole vygenerovaný token, který najdu na ploše v poznámkovém bloku.

Za blok http zapojím blok function do něj vložím tento kód
var count = 0;
for (var i = 0; i < msg.payload.features.length; i++) {
    count += msg.payload.features[i].properties.delay;
}
var prumer = count / msg.payload.features.length;
msg.payload = prumer;
return msg;


var znamená "vytvoř novou proměnnou". -> Používá se k tomu, aby si program uložil nějakou hodnotu, se kterou dál pracuje.
for znamená opakuj něco víckrát – tedy cyklus. -> Používá se, když chceš projít všechny položky v seznamu (např. všechny autobusy).
msg.payload znamená hlavní obsah zprávy v Node-RED. ->Používá se k předávání dat mezi bloky.
return msg znamená: pošli zprávu dál do dalšího bloku. -> Používá se na konci function bloku, aby výstup pokračoval v toku (flow). Bez toho by data nepokračovala dál.


Jako poslední blok za function zapojím debug. Pokud chci mít kontrolu nad tím, jaká data přichází z golemia můžu vložit ještě jeden debug za http request

Dám vpravo nahoře deploy -> 
Následně kliknu na tlačítko u programovacího bloku timestamp a zkontroluju data, která mi vychází vpravo v nabídce debug

15. A máme hotovo!





### 18. Maturitní otázka
18.MATURITNÍ OTÁZKA
Zadání: 18. Praktické cvičení v programu Node-Red – práce s Real-Time daty, zpracování dat pomocí funkce, práce s mapou. Teorie REST API.
 Nastavte datovou sadu na webové stránce https://golemioapi.docs.apiary.io/ tak, aby do vašeho řešení v programu Node-red přicházela data o aktuální pozici všech autobusů na lince 176 a všech jejich bývalých pozic. Poté se pokuste vykreslit do mapy aktuální polohu prvního autobusu v poli. Autorizační klíč máte k dispozici na ploše počítače v textovém souboru.
Připravím si blok inject/timestamp, který následně „vysílá“ signál a spouští reakce.
Následně si připravím blok http request, který následně získává data z golemia. Blok vyšle „poptávku“ do golemia a čeká na odpověď.
Otevřu si stránku api.golemio -> public vehicle positions -> přihlásím se pomocí x-access-tokenu, který najdu na ploše v poznámkovém bloku
Kliknu na try-it-out a změním předvyplněný údaj (číslo autobusu a transport type) na linku 176 a bus. Nic jiného neměním. 

Kliknu na execute a zkopíruji odkaz

Odkaz vložím do bloku http request do řádku URL

Ve stejném bloku o kus níže založím nový header a v kolonce nad změním na JSON object. Do prvního pole headers zadám X-Access-Token a do druhého pole vygenerovaný token, který najdu na ploše v poznámkovém bloku.

Za blok http zapojím blok function do něj vložím tento kód
msg.payload = { 
   "name": "Linka 176", 
    "lat": msg.payload.features[0].geometry.coordinates[1], 
    "lon": msg.payload.features[0].geometry.coordinates[0] 
} 
return msg; 


msg.payload znamená hlavní obsah zprávy v Node-RED. ->Používá se k předávání dat mezi bloky.
lat znamená zeměpisná šířka (latitude) – určuje, jak vysoko na mapě místo je.
lon znamená zeměpisná délka (longitude) – určuje, jak vpravo nebo vlevo na mapě místo je.
return msg znamená: pošli zprávu dál do dalšího bloku. -> Používá se na konci function bloku, aby výstup pokračoval v toku (flow). Bez toho by data nepokračovala dál.
Jako poslední blok za function zapojím worldmap (Pokud není mapa v nabídce vlevo musím jí stáhnout). Pokud chci mít kontrolu nad tím, jaká data přichází z golemia můžu vložit ještě jeden debug za http request.

Dám vpravo nahoře deploy -> 
Poté stisknu tlačítko u bloku timestamp
Následně si zkopíruju odkaz, jako na obrázku, za lomítko dopíšu worldmap. Otevřu v novém okně a zkontroluji, zda se mi propisují správně data.


A máme hotovo!
 

### 19. Maturitní otázka
19.MATURITNÍ OTÁZKA
Zadání: 19. Praktické cvičení v programu Node-Red – práce s Real-Time daty, tvorba dashboardu, uživatelský vstup, ošetření výjimek. Práce s jednorozměrnými a dvourozměrnými poli. 
Pokuste se sestavit řešení v programu Node-red, které umožní uživateli pomocí textového pole v dashboardu vložit číslo linky autobusu a na základě tohoto údaje se vypíše pomocí grafu typu gauge aktuální zpoždění prvního autobusu v poli na uvedené lince. Zároveň se pokuste ošetřit nodem možné výjimky. Autorizační klíč máte k dispozici na ploše počítače v textovém souboru. Nastavte datovou sadu na webové stránce https://api.golemio.cz/v2/pid/docs/openapi/ tak, aby do vašeho řešení v programu Node-red přicházela data o aktuální pozici autobusů včetně jejich zpoždění.
Přetáhnu na plochu blok text input
Ten otevřu a přidám novou skupinu, tu pojmenuju.
  ->
-> 
Za to zapojím http request
 
Otevřu si stránku api.golemio -> public vehicle positions -> přihlásím se pomocí x-access-tokenu, který najdu na ploše v poznámkovém bloku
Kliknu na try-it-out a změním předvyplněný údaj (číslo autobusu a transport type) na linku 176 a bus. Nic jiného neměním. 
Do URL odkazu místo čísla autobusu vložím {{payload}}
Dolů vložím klasicky do header X-Access-Token a svůj zkopírovaný odkaz z golemia, které najdu na ploše v textovém poli






Dál zapojím funkci a do ní vložím tento kód 
if(msg.payload.features != undefined){
msg.payload = msg.payload.features[0].properties.delay;
}else{
    msg.payload = "NEEXISTUJE!";
}
return msg;


Jako další zapojím dashboardu blok gauge a ten pojmenuji zpozdeni autobusu v sekundách a nastavím max na 360 sekund. V kolonce group vyberu možnost, kterou jsem založila na začátku v text inputu. Můžu i upravit barvy. 

Odešlu deploy

Následně otevřu pod debugem tuto šipku a kliknu na dashboard 

Potom otevřu tuto „odkazovou“ šipku a ta mě hodí na webovou stránku s grafem, kde můžu zkusit zadat číslo jakéhokoli autobusu, kter existuje a vyhodí mi to jeho aktuální zpoýdění v sekundách


A máme hotovo!

### 20. Maturitní otázka
20.MATURITNÍ OTÁZKA
Zadání: 20. Praktické cvičení v programu Node-Red – práce s Real-Time daty, synchronní a asynchronní odesílání zpráv. Analýza dat a nastavení notifikací. 
https://api.golemio.cz/v2/pid/docs/openapi/ tak, aby do vašeho řešení v programu Node-red přicházela data o aktuální pozici všech autobusů na lince 176 a jejich aktuální odchylce od jízdního řádu. Poté se pokuste asynchronním způsobem vypsat do debugu aktuální odchylku každého autobusu na lince. Autorizační klíč máte k dispozici na ploše počítače v textovém souboru.
Připravím si blok inject/timestamp, který následně „vysílá“ signál a spouští reakce.
Následně si připravím blok http request, který následně získává data z golemia. Blok vyšle „poptávku“ do golemia a čeká na odpověď.
Otevřu si stránku api.golemio -> public vehicle positions -> přihlásím se pomocí x-access-tokenu, který najdu na ploše v poznámkovém bloku
Kliknu na try-it-out a změním předvyplněný údaj (číslo autobusu a transport type) na linku 176 a bus. Nic jiného neměním. 

Kliknu na execute a zkopíruji odkaz

Odkaz vložím do bloku http request do řádku URL





Ve stejném bloku o kus níže založím nový header a v kolonce nad změním na JSON object. Do prvního pole headers zadám X-Access-Token a do druhého pole vygenerovaný token, který najdu na ploše v poznámkovém bloku.

Za blok http zapojím blok function do něj vložím tento kód
var count = 0;
for (var i = 0; i < msg.payload.features.length; i++) {
    count += msg.payload.features[i].properties.delay;
}
var prumer = count / msg.payload.features.length;
msg.payload = prumer;
return msg;


var znamená "vytvoř novou proměnnou". -> Používá se k tomu, aby si program uložil nějakou hodnotu, se kterou dál pracuje.
for znamená opakuj něco víckrát – tedy cyklus. -> Používá se, když chceš projít všechny položky v seznamu (např. všechny autobusy).
msg.payload znamená hlavní obsah zprávy v Node-RED. ->Používá se k předávání dat mezi bloky.
return msg znamená: pošli zprávu dál do dalšího bloku. -> Používá se na konci function bloku, aby výstup pokračoval v toku (flow). Bez toho by data nepokračovala dál.


Jako poslední blok za function zapojím debug. Pokud chci mít kontrolu nad tím, jaká data přichází z golemia můžu vložit ještě jeden debug za http request

Dám vpravo nahoře deploy -> 
Následně kliknu na tlačítko u programovacího bloku timestamp a zkontroluju data, která mi vychází vpravo v nabídce debug

15. Toto je příklad tzv. synchronního zapojení. Synchronní zapojení odešle z funkčního bloku „požadavek“ do golemia a čeká na odpověď. Dokud nedostane odpověď, nepokračuje
16. Asynchronní zapojení v tomto případě nejde, jelikož bez live dat nemůže node-red zjistit aktuální polohu autobusů
17. A máme hotovo!


## Mosaic

### 11. Maturitní otázka
11.MATURITNÍ OTÁZKA
Zadání: 11. Síťová technika, přenosová media, pasivní a aktivní síťové prvky, zabezpečení komunikace, rušení. Zamyslete se nad způsobem párování bezdrátových prvků. Jakým způsobem připojíme bezdrátové prvky do zbytku sítě v chytrém domě. Výhody a nevýhody bezdrátových sítí. 
Síťová technika 
Zabývá se návrhem, instalací, konfigurací a údržbou počítačových sítí. 
Zahrnuje prvky jako routery (Router je krabička, která připojuje zařízení k internetu a rozvádí Wi-Fi.), switche (Switch je krabička, která propojuje více zařízení v jedné síti, aby si mohla mezi sebou posílat data), síťové kabely, síťové karty a další hardware potřebný pro propojení zařízení v síti. 
Přenosová média 
Jsou prostředky, kterými se data přenášejí v síti.  
Kabelová média: např. ethernetové kabely (UTP- nestíněné, STP - stíněné), optická vlákna. 
Bezdrátová média: Wi-Fi, Bluetooth, radiové vlny, infračervené záření. 
Pasivní a aktivní síťové prvky 
Pasivní prvky – nemají vlastní zdroj napájení, pouze přenášejí signál.  
Příklady: kabely, konektory, patch panely. 
Aktivní prvky – vyžadují napájení a aktivně zpracovávají data.  
Příklady: routery, switche, přístupové body (Access Points). 
Zabezpečení komunikace 
Ochrana sítě a přenosu dat před neautorizovaným přístupem a útoky.  
Šifrování – zajišťuje, že data jsou přenášena v zašifrované podobě. 
Autentizace – ověření identity uživatele nebo zařízení. 
Firewall – chrání síť před neoprávněnými přístupy zvenčí. 
Rušení 
Rušení je nežádoucí vliv, který narušuje přenos signálu v síti.  
Může být způsobeno překážkami (zdi, nábytek), dalšími zařízeními (mikrovlnné trouby, Bluetooth zařízení) nebo i počasím (např. bouřky). 
Rušení může způsobit ztrátu signálu, zpomalení komunikace nebo výpadky připojení. 

Odpovězte na otázky: a. Jaké jsou výhody a nevýhody bezdrátového připojení oproti kabelu. b. Jakým způsobem připojíme bezdrátové prvky do zbytku sítě? c. Co je to rušení? d. Kdy použijeme bezdrátové připojení v chytrém domě a kdy kabel? e. Jaké další bezdrátové sítě znáte? Rozdíly, topologie?
a. Jaké jsou výhody a nevýhody bezdrátového připojení oproti kabelu? 
Výhody: 
Mobilita a flexibilita – zařízení mohou být připojena odkudkoli v dosahu sítě. 
Snadná instalace – není potřeba pokládat kabely. 
Možnost připojení více zařízení bez nutnosti fyzických zásahů. 
Nevýhody: 
Nižší rychlost a stabilita oproti kabelovému připojení. 
Vyšší náchylnost k rušení (od jiných zařízení nebo překážek). 
Bezpečnostní rizika – bezdrátové sítě mohou být snáze napadnutelné. 
 
b. Jakým způsobem připojíme bezdrátové prvky do zbytku sítě? 
Bezdrátové prvky se připojují pomocí Wi-Fi routeru nebo přístupového bodu (Access Point), který zajišťuje komunikaci mezi bezdrátovými zařízeními a zbytkem sítě. 
V chytrém domě mohou být zařízení připojena pomocí protokolů jako Wi-Fi, Bluetooth, Zigbee nebo Z-Wave. 
 
c. Co je to rušení? 
Rušení je jev, kdy externí signály (např. od jiných elektronických zařízení) narušují bezdrátovou komunikaci. 
Může způsobit zpomalení přenosu dat, ztrátu signálu nebo přerušení spojení. 
 
d. Kdy použijeme bezdrátové připojení v chytrém domě a kdy kabel? 
Bezdrátové připojení použijeme, když je potřeba mobilita zařízení (např. kamery, senzory, osvětlení). 
Kabelové připojení se hodí tam, kde požadujeme vyšší stabilitu a rychlost (např. u hlavního serveru, chytré televize nebo domácího úložiště NAS). 
 
e. Jaké další bezdrátové sítě znáte? Rozdíly, topologie? 
Bluetooth – krátký dosah, nízká spotřeba energie. 
Zigbee – vhodné pro chytré domácnosti, nízká spotřeba energie, topologie mesh. 
Z-Wave – podobné jako Zigbee, ale s delším dosahem. 
NFC (Near Field Communication) – velmi krátký dosah, používané pro bezkontaktní platby. 
LoRaWAN – síť s dlouhým dosahem a nízkou spotřebou energie, vhodná pro IoT zařízení. 


### 12. Maturitní otázka
12.MATURITNÍ OTÁZKA
Zadání: 12. Praktické krimpování konektorů, zapojení keystonů. Teorie sériové komunikace, sběrnice CIB. a. Co je to komunikační protokol? A jaké znáte? b. Co je to komunikační protokol? TCP, UDP? c. Co je to sériová komunikace? d. Popište komunikační standard Modbus e. Co je rack a patchpanel? f. Kabeláž, PoE, dělení kroucené dvojlinky

a. Co je to komunikační protokol? A jaké znáte?
Komunikační protokol je soubor pravidel, který určuje, jak si zařízení mezi sebou předávají data.
Zajišťuje správné formátování, odesílání a přijetí zpráv mezi zařízeními.
Známé protokoly: Modbus, BACnet, KNX, MQTT, HTTP, FTP, TCP/IP, UDP, CAN, CIB (TECO).
b. Co je to komunikační protokol TCP, UDP?
TCP (Transmission Control Protocol):
Spojovaný protokol – navazuje spojení, zajišťuje spolehlivý přenos dat (kontrola chyb, doručení).
Používá se např. u webových stránek (HTTP), e-mailu, FTP.
UDP (User Datagram Protocol):
Nespojovaný – rychlý, ale nespolehlivý přenos, bez potvrzení.
Vhodné pro streaming, VoIP nebo herní servery, kde je důležitá rychlost.
c. Co je to sériová komunikace?
Způsob přenosu dat bit (1/0 -> 8bitů= byte) po bitu (sekvenčně) jedním vodičem (nebo dvojicí).
Používá se tam, kde není potřeba vysoká rychlost nebo šířka pásma.
Typické protokoly: RS-232, RS-485, Modbus RTU, UART, USB
Využití: PLC, měřicí zařízení, průmyslové sběrnice.
Přechod z paralelních rozhraní na sériovou komunikaci
          
d. Popište komunikační standard Modbus
Modbus je průmyslový komunikační protokol založený na sériové komunikaci (RS-485) nebo TCP/IP.
Funguje v režimu Master–Slave (jeden hlavní, více podřízených).
Přenáší data ve formě registrů (adresy), často používaný pro senzory, měřiče a PLC.
Verze: Modbus RTU (sériově), Modbus TCP (po síti).
e. Co je rack a patchpanel?
Rack: kovová skříň nebo rám, kde jsou uchyceny aktivní a pasivní síťové prvky (routery, switche, servery).
Patchpanel: pasivní panel s konektory (např. RJ-45), který slouží k organizaci a propojení kabeláže v racku.
Umožňuje snadné spravování kabeláže pomocí krátkých patch kabelů.
  
f. Kabeláž, PoE, dělení kroucené dvojlinky
Kroucená dvojlinka (UTP, STP, FTP):
Kabel složený z párů vodičů, které jsou vzájemně kroucené pro snížení rušení.
UTP – nechráněná, FTP/STP – stíněná proti rušení.
PoE (Power over Ethernet):
Technologie, která umožňuje napájet zařízení (např. IP kamery, WiFi) přes stejný kabel, kterým se přenáší data.
Zjednodušuje instalaci, nepotřebuje samostatné napájecí kabely.
Dělení kabelů podle kategorie (Cat5e, Cat6, Cat6A, Cat7):
Určují maximální přenosovou rychlost a šířku pásma.
                    		








### 13. Maturitní otázka
13.MATURITNÍ OTÁZKA
13. Teorie automatizace (stupně automatizace, typy automatizace, důvody a dopady automatizace), teorie centralizovaných/decentralizovaných systémů řízení. a. Do jakého stupně automatizace by zařadil otevírání dveří v obchodě a do jakého alarm. b. Rozdíl mezi cent. A decent řízením c. Stupně automatizace (Automatické ovládání, regulace, řízení) d. Historie automatizace

Automatizace:
proces, při kterém dochází k nahrazování lidské činnosti stroji, softwarem nebo jinými technologiemi. Cílem je zvýšení efektivity, snížení nákladů, minimalizace chyb a zvýšení bezpečnosti, zmenšení lidské práce na dané činnosti.
Krok následující po mechanizaci
Automatizovaný proces:
Vychází ze senzorických dat
Typy automatizace:
Pevná(hardwarová) - Specializované stroje pro jednu konkrétní činnost (např. montážní linky v automobilkách). 
Programovatelná - Lze ji přizpůsobit různým úkolům změnou softwaru (např. CNC stroje). 
Flexibilní - Systém se sám přizpůsobuje měnícím se požadavkům (např. moderní robotické výrobní linky). 
Důvody a dopady automatizace:
Důvody:
Zvýšení produktivity 
Snížení nákladů na pracovní sílu 
Zlepšení kvality a přesnosti výroby 
Zvýšení bezpečnosti práce 
Minimalizace lidských chyb 
Dopady:
Úbytek pracovních míst v některých odvětvích 
Zvýšené nároky na kvalifikaci pracovníků 
Snížení chybovosti a zvýšení efektivity 
Počáteční vysoké investiční náklady 











TEORIE CENTRALIZOVANÝCH A DECENTRALIZOVANÝCH SYSTÉMŮ ŘÍZENÍ

Rozdíl mezi centralizovaným a decentralizovaným řízením: 
Centralizované řízení 
Všechna rozhodnutí dělá jedno centrální řídicí místo (např. server, PLC). 
Výhodou je snadná kontrola a správa. 
Nevýhodou je větší riziko selhání celého systému při poruše. 
Příklad: starší výrobní linky, centrální dispečink energetické sítě. 
Decentralizované řízení 
Každá část systému funguje autonomně a komunikuje s ostatními jednotkami. 
Výhodou je vyšší spolehlivost a flexibilita. 
Nevýhodou může být složitější koordinace a vyšší náklady na komunikaci mezi prvky. 
Příklad: moderní chytré továrny, blockchain. 


a. Do jakého stupně automatizace by zařadil otevírání dveří v obchodě a do jakého alarm? 
Otevírání dveří v obchodě → Automatické ovládání, protože senzor pouze vyšle signál ke spuštění akce (otevření dveří). 
Alarm → Automatická regulace, pokud reaguje na podněty (např. pohybový senzor spustí sirénu). Pokud alarm sám analyzuje situaci a rozhoduje o dalším postupu, může spadat do automatického řízení (např. bezpečnostní systém s kamerami a AI). 
b. Rozdíl mezi centralizovaným a decentralizovaným řízením 
centralizované systémy mají jedno hlavní řídicí centrum, zatímco decentralizované systémy rozdělují řízení mezi více autonomních jednotek. 
c. Stupně automatizace (Automatické ovládání, regulace, řízení) 
Automatické ovládání – Provádí jednoduché akce na základě podnětu (např. světlo na fotobuňku, splachování, samootvírací dveře). 
Automatická regulace – Udržuje určitou veličinu v požadovaném stavu (např. termostat). 
Automatické řízení – Rozhoduje se na základě složitější analýzy (např. autonomní vozidlo). 
d. Historie automatizace 
Průmyslová revoluce (18. a 19. století) – První mechanizované stroje, např. parní stroje. 
20. století – Automatizace výroby, montážní linky (např. Henry Ford). 
Počítačová automatizace (2. pol. 20. století) – Vznik programovatelných řídicích jednotek (PLC), CNC strojů. 
Dnešní doba – Umělá inteligence, IoT, autonomní systémy. 


### 14. Maturitní otázka
14.MATURITNÍ OTÁZKA
Zadání: 14. Umělé osvětlení. Vliv umělého osvětlení na lidské zdraví. Spektrální složení světla podle typů svítidel. Umístění světelných zdrojů ve vnitřních prostorách. Světelné znečištění. Odpovězte na otázky: a. Typy svítidel? b. Parametry osvětlení c. Vliv barvy světla na člověka d. Spektrální složení světla podle typu světel e. Jak umístit světla f. Co je to světelné znečištění, jak vzniká a jak ho eliminovat
a) Typy svítidel 
Svítidla můžeme rozdělit podle různých kritérií: 
Podle světelného zdroje: 
Žárovkové – klasické a halogenové žárovky 
Výbojkové – zářivky, sodíkové a rtuťové výbojky 
LED – moderní LED technologie 
Podle směrování světla: 
Přímá (světlo míří přímo dolů) 
Nepřímá (odráží se od stropu/stěn) 
Smíšená 
Podle použití: 
Interiérová (stropní, stolní, bodová) 
Exteriérová (pouliční, reflektory, fasádní osvětlení) 
b) Parametry osvětlení 
Intenzita světla (lx – luxy) – množství světla dopadajícího na plochu 
Teplota chromatičnosti (K – Kelvin) – určuje, zda je světlo teplé (žluté) nebo studené (modré) 
Index podání barev (CRI – Color Rendering Index) – jak věrně světlo zobrazuje barvy 
Účinnost (lm/W – lumeny na watt) – kolik světla svítidlo vyprodukuje vzhledem ke spotřebované energii 
c) Vliv barvy světla na člověka 
Teplé světlo (2700–3500 K) – uklidňuje, vhodné do ložnic a obývacích pokojů 
Neutrální světlo (4000–5000 K) – přirozené světlo, vhodné do kanceláří a pracoven 
Studené světlo (5500 K a více) – stimuluje pozornost, vhodné do nemocnic, škol, průmyslových prostor 
Modré světlo (LED, displeje) může narušovat spánek tím, že potlačuje tvorbu melatoninu. 
d) Spektrální složení světla podle typu světel 
Žárovkové světlo – plynulé spektrum, blízké slunečnímu světlu 
Zářivky a výbojky – nespojité spektrum, mohou zkreslovat barvy 
LED světlo – různé spektrální složení podle typu čipu, často obsahuje hodně modré složky 
e) Jak umístit světla 
V obytných prostorech – kombinace stropního, bodového a ambientního osvětlení 
V kancelářích – rovnoměrné osvětlení s minimem odlesků 
V exteriéru – správně směrované světlo, aby neoslňovalo a minimalizovalo světelné znečištění 
f) Co je to světelné znečištění, jak vzniká a jak ho eliminovat 
Vzniká nadměrným a špatně směrovaným umělým osvětlením 
Dopady:  
Rušení nočního ekosystému (ptáci, hmyz) 
Negativní vliv na spánek a zdraví lidí 
Plýtvání energií 
Řešení: 
Používat světla s teplou barevnou teplotou 
Omezit zbytečné osvětlování 
Používat směrová svítidla a správné časování 
 


### 15. Maturitní otázka
15.MATURITNÍ OTÁZKA
15. Vliv kvality ovzduší na lidské zdraví (oxid uhličitý, těkavé látky, těžké kovy, teplota, vlhkost), doporučené parametry vnitřního ovzduší. Způsoby monitorování ovzduší.
Znečištěné ovzduší způsobuje vážná onemocnění 
Dlouhodobé vystavení škodlivinám (oxidům dusíku, těžkým kovům, prachu) zvyšuje riziko rakoviny, respiračních a kardiovaskulárních chorob.  
Kvalita venkovního ovzduší (ovlivněna výskytem aut, továren, elektráren apod. v okolí) 
Kvalita vnitřního ovzduší (četnost větrání)

CO₂ – bolesti hlavy a únava 
Nad 1000 ppm způsobuje únavu, bolesti hlavy a zhoršené soustředění. 
Řešením je časté větrání nebo ventilační systémy.  
Vyskytuje se nadměrně často např. v kancelářích

Těkavé organické látky (TVOCs) – nebezpečné výpary  
Uvolňují se z čisticích prostředků, nábytku nebo cigaretového kouře. 
Způsobují nevolnost, poškození jater/ledvin a rakovinu. 
Omezte chemikálie a větrejte, používejte přírodní čisticí prostředky, v průmyslech kde se vyskytují je potřeba si chránit dýchací cesty

Těžké kovy – neurotoxicita a rakovina 
Olovo, rtuť a kadmium poškozují nervový systém, zejména u dětí. 
Vyskytují se v průmyslu a dopravě. 
Vyšší v oblastech s frekventovanou dopravou, nebo v blízkosti průmyslových závodů. 
Nutná je ochrana dýchacích cest.  
U dětí způsobují vývojové poruchy, a poškozují kongitivní rozvoj. Způsobují závažná ongologická onemocnění.

Jemné prachové částice (PM2.5 a PM10) – poškození plic 
PM2.5 způsobuje astma
PM10 poškozuje plíce
Vznikají při spalování paliv a stavebních pracích. 
Chraňte se respirátory.  

Vlhkost a teplota ovlivňují pohodu 
Ideální teplota: 20–26 °C
vlhkost: 40–60 %. 
Příliš suchý vzduch dráždí dýchací cesty, vysoká vlhkost podporuje plísně.  
Teplota má vliv na soustředění a únavu, výšší nebo nížší teplota může mít negativní dopad na produktivitu.  

Monitorování kvality ovzduší 
Lze provádět automaticky pomocí technologií chytrých domů.
Chytré senzory měří CO₂, TVOCs, prach a vlhkost. 
Automatické větrací systémy zlepšují kvalitu vzduchu v budovách. 
V továrnách využívání varovných sýstémů při výskytu toxcických látek.

Tip na zapamatování:  
CO₂ = větrat  
TVOCs = méně chemie  
Těžké kovy = respirátory  
Prach = filtrace vzduchu  
Vlhkost 40–60 % = zdravé prostředí 
 


### 16. Maturitní otázka
16.MATURITNÍ OTÁZKA
Zadání: 16. Historie průmyslových revolucí a vývoje oboru.
Historie průmyslových revolucí a vývoje oboru chytré domy 

1. Průmyslové revoluce 
Průmyslové revoluce představují klíčové mezníky v technologickém a hospodářském rozvoji lidstva. 

První průmyslová revoluce (18. - 19. století) 
Přechod od ruční výroby k mechanizaci a tovární výrobě. 
Využití parního stroje (James Watt) a rozvoj textilního průmyslu. 
Zavedení železnic a parní dopravy, což umožnilo rychlejší přepravu zboží a osob. 
Druhá průmyslová revoluce (konec 19. století – začátek 20. století) 
Zavedení elektřiny do průmyslu a domácností. 
Vznik montážních linek (Henry Ford) a masová výroba. 
Vývoj spalovacích motorů a telefonní komunikace. 
Třetí průmyslová revoluce (polovina 20. století – přelom 21. století) 
Digitalizace, vznik počítačů a automatizace průmyslu. 
Nástup internetu, který způsobil zásadní změny v komunikaci. 
První koncepty inteligentních domů s programovatelnými zařízeními. 
Čtvrtá průmyslová revoluce (současnost – 21. století) 
Internet věcí (IoT), umělá inteligence a big data. 
Propojení zařízení v chytrých domech pomocí senzorů a sítí. 
Automatizace a robotizace v běžném životě. 


2. Vývoj oboru chytré domy 
Obor chytrých domů prošel významným vývojem v návaznosti na průmyslové revoluce: 
Počátky chytrých domů (20. století) 
V 60. a 70. letech byly první pokusy o domácí automatizaci (např. centrální ovládání vytápění). 
V 90. letech se objevily první propojené systémy domácí automatizace řízené počítači. 
Rozvoj chytrých domů (začátek 21. století) 
Vznik bezdrátových technologií (Wi-Fi, Bluetooth, Zigbee) umožnil širší využití smart zařízení. 
První domácí asistenti jako Amazon Echo (2014) nebo Google Home (2016) přinesli hlasové ovládání. 
Vývoj aplikací pro vzdálené ovládání domácích zařízení. 
 
Současnost a budoucnost chytrých domů 
Využití umělé inteligence pro prediktivní řízení spotřeby energie a bezpečnosti. 
Rozšíření chytrých domácích spotřebičů (chytré termostaty, zámky, osvětlení, senzory kvality vzduchu). 
Ekologické aspekty chytrých domů – solární panely, energeticky efektivní systémy řízení. 
3. Závěr 
Vývoj chytrých domů úzce souvisí s průmyslovými revolucemi, zejména s digitalizací a internetem věcí. V budoucnu lze očekávat širší využití umělé inteligence, autonomních systémů a ekologických technologií pro efektivní a udržitelný provoz chytrých domácností. 

