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
