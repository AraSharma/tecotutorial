20.MATURITNÍ OTÁZKA
Zadání: 20. Praktické cvičení v programu Node-Red – práce s Real-Time daty, synchronní a asynchronní odesílání zpráv. Analýza dat a nastavení notifikací. 

https://api.golemio.cz/v2/pid/docs/openapi/ tak, aby do vašeho řešení v programu Node-red přicházela data o aktuální pozici všech autobusů na lince 176 a jejich aktuální odchylce od jízdního řádu. Poté se pokuste asynchronním způsobem vypsat do debugu aktuální odchylku každého autobusu na lince. Autorizační klíč máte k dispozici na ploše počítače v textovém souboru.

Připravím si blok inject/timestamp, který následně „vysílá“ signál a spouští reakce.

Následně si připravím blok http request, který následně získává data z golemia. Blok vyšle „poptávku“ do golemia a čeká na odpověď.

Otevřu si stránku api.golemio -> public vehicle positions -> přihlásím se pomocí x-access-tokenu, který najdu na ploše v poznámkovém bloku

Kliknu na try-it-out a změním předvyplněný údaj (číslo autobusu a transport type) na linku 176 a bus. Nic jiného neměním. 

<img width="795" alt="Snímek obrazovky 2568-05-28 v 13 39 16" src="https://github.com/user-attachments/assets/8c65d9d7-edca-41b3-b0c6-378ab450a01b" />

Kliknu na execute a zkopíruji odkaz

<img width="841" alt="Snímek obrazovky 2568-05-28 v 13 40 12" src="https://github.com/user-attachments/assets/8a39b2d8-6ad0-4b41-aa29-a8d2acecbecf" />

Odkaz vložím do bloku http request do řádku URL

<img width="528" alt="Snímek obrazovky 2568-05-28 v 13 41 31" src="https://github.com/user-attachments/assets/d1ccc996-5f5e-4693-b807-7ff3215339dc" />




Ve stejném bloku o kus níže založím nový header a v kolonce nad změním na JSON object. Do prvního pole headers zadám X-Access-Token a do druhého pole vygenerovaný token, který najdu na ploše v poznámkovém bloku.
<img width="474" alt="Snímek obrazovky 2568-05-28 v 13 42 04" src="https://github.com/user-attachments/assets/a273489d-24ec-436c-9395-afb9f8384580" />

Za blok http zapojím blok function do něj vložím tento kód

  var count = 0;
  for (var i = 0; i < msg.payload.features.length; i++) {
    count += msg.payload.features[i].properties.delay;
  }
  var prumer = count / msg.payload.features.length;
  msg.payload = prumer;
  return msg;

<img width="544" alt="Snímek obrazovky 2568-05-28 v 13 44 20" src="https://github.com/user-attachments/assets/00577e88-8c8c-42fc-81ff-6eab19bf7480" />


var znamená "vytvoř novou proměnnou". -> Používá se k tomu, aby si program uložil nějakou hodnotu, se kterou dál pracuje.
for znamená opakuj něco víckrát – tedy cyklus. -> Používá se, když chceš projít všechny položky v seznamu (např. všechny autobusy).
msg.payload znamená hlavní obsah zprávy v Node-RED. ->Používá se k předávání dat mezi bloky.
return msg znamená: pošli zprávu dál do dalšího bloku. -> Používá se na konci function bloku, aby výstup pokračoval v toku (flow). Bez toho by data nepokračovala dál.


Jako poslední blok za function zapojím debug. Pokud chci mít kontrolu nad tím, jaká data přichází z golemia můžu vložit ještě jeden debug za http request
<img width="653" alt="Snímek obrazovky 2568-05-28 v 13 44 54" src="https://github.com/user-attachments/assets/3b268755-ddc2-4efd-839f-cd0cbb2a8167" />

Dám vpravo nahoře deploy -> 
Následně kliknu na tlačítko u programovacího bloku timestamp a zkontroluju data, která mi vychází vpravo v nabídce debug
<img width="376" alt="Snímek obrazovky 2568-05-28 v 13 46 07" src="https://github.com/user-attachments/assets/3c360029-687e-4f48-913a-5fa6776c31e4" />

15. Toto je příklad tzv. synchronního zapojení. Synchronní zapojení odešle z funkčního bloku „požadavek“ do golemia a čeká na odpověď. Dokud nedostane odpověď, nepokračuje
16. Asynchronní zapojení v tomto případě nejde, jelikož bez live dat nemůže node-red zjistit aktuální polohu autobusů
17. A máme hotovo!
