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
