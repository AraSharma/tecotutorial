Zadání: 18. Praktické cvičení v programu Node-Red – práce s Real-Time daty, zpracování dat pomocí funkce, práce s mapou. Teorie REST API.

 Nastavte datovou sadu na webové stránce https://golemioapi.docs.apiary.io/ tak, aby do vašeho řešení v programu Node-red přicházela data o aktuální pozici všech autobusů na lince 176 a všech jejich bývalých pozic. Poté se pokuste vykreslit do mapy aktuální polohu prvního autobusu v poli. Autorizační klíč máte k dispozici na ploše počítače v textovém souboru.

Připravím si blok inject/timestamp, který následně „vysílá“ signál a spouští reakce.

Následně si připravím blok http request, který následně získává data z golemia. Blok vyšle „poptávku“ do golemia a čeká na odpověď.

Otevřu si stránku api.golemio -> public vehicle positions -> přihlásím se pomocí x-access-tokenu, který najdu na ploše v poznámkovém bloku

Kliknu na try-it-out a změním předvyplněný údaj (číslo autobusu a transport type) na linku 176 a bus. Nic jiného neměním. 

<img width="775" alt="Snímek obrazovky 2568-05-28 v 13 16 49" src="https://github.com/user-attachments/assets/3613c329-fb09-499b-8eb3-1709f241f95d" />


Kliknu na execute a zkopíruji odkaz

<img width="786" alt="Snímek obrazovky 2568-05-28 v 13 18 30" src="https://github.com/user-attachments/assets/6bf9fe1e-4042-499c-8310-d60dfc120d50" />


Odkaz vložím do bloku http request do řádku URL

<img width="471" alt="Snímek obrazovky 2568-05-28 v 13 18 54" src="https://github.com/user-attachments/assets/57fdb8c0-d2ba-4d39-98d0-3f2a6b9b6ef0" />


Ve stejném bloku o kus níže založím nový header a v kolonce nad změním na JSON object. Do prvního pole headers zadám X-Access-Token a do druhého pole vygenerovaný token, který najdu na ploše v poznámkovém bloku.

<img width="317" alt="Snímek obrazovky 2568-05-28 v 13 19 27" src="https://github.com/user-attachments/assets/e96d4e37-8817-4539-bcc8-058a3e915519" />


Za blok http zapojím blok function do něj vložím tento kód

msg.payload = { 

   "name": "Linka 176", 

    "lat": msg.payload.features[0].geometry.coordinates[1], 

    "lon": msg.payload.features[0].geometry.coordinates[0] 

} 

return msg; 

<img width="573" alt="Snímek obrazovky 2568-05-28 v 13 20 13" src="https://github.com/user-attachments/assets/9839279a-325b-4dd7-8671-90c5753edc5e" />




msg.payload znamená hlavní obsah zprávy v Node-RED. ->Používá se k předávání dat mezi bloky.

lat znamená zeměpisná šířka (latitude) – určuje, jak vysoko na mapě místo je.

lon znamená zeměpisná délka (longitude) – určuje, jak vpravo nebo vlevo na mapě místo je.

return msg znamená: pošli zprávu dál do dalšího bloku. -> Používá se na konci function bloku, aby výstup pokračoval v toku (flow). Bez toho by data nepokračovala dál.

Jako poslední blok za function zapojím worldmap (Pokud není mapa v nabídce vlevo musím jí stáhnout). Pokud chci mít kontrolu nad tím, jaká data přichází z golemia můžu vložit ještě jeden debug za http request.

<img width="647" alt="Snímek obrazovky 2568-05-28 v 13 20 47" src="https://github.com/user-attachments/assets/1cb84b90-73da-4a7b-a3b8-c59c2b1385d2" />


Dám vpravo nahoře deploy -> 

Poté stisknu tlačítko u bloku timestamp

Následně si zkopíruju odkaz, jako na obrázku, za lomítko dopíšu worldmap. Otevřu v novém okně a zkontroluji, zda se mi propisují správně data.
<img width="379" alt="Snímek obrazovky 2568-05-28 v 13 21 12" src="https://github.com/user-attachments/assets/b4c59199-f3a5-4b6e-8310-ee534dc997e5" />





A máme hotovo!

 

