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

 

