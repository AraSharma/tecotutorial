Zadání:**  
17. Praktické cvičení v programu Node-Red – práce s API, přístupový token, zpracování dat pomocí funkce, výpis dat.  
Teorie způsobu zápisu dat JSON, porovnání s XML.

---

## Postup:

1. Nastavte datovou sadu na webové [https://api.golemio.czv2/pid/docs/openapi/ tak, aby do vašeho řešení v programu Node-RED přicházela data o aktuální pozici všech autobusů na lince 176 a jejich aktuální odchylce od jízdního řádu.

2. Poté se pokuste vypsat do debugu průměrnou hodnotu odchylky všech autobusů na lince 176 v danou chvíli. Autorizační klíč máte k dispozici na ploše počítače v textovém souboru.

3. Připravím si blok `inject/timestamp`, který následně „vysílá“ signál a spouští reakce.

4. Následně si připravím blok `http request`, který získává data z Golemia. Blok vyšle „poptávku“ do Golemia a čeká na odpověď.

5. Otevřu si stránku API Golemio → *public vehicle positions* → přihlásím se pomocí `X-Access-Token`, který najdu na ploše v poznámkovém bloku.

6. Kliknu na **Try it out** a změním předvyplněný údaj (číslo autobusu a `transport type`) na linku **176** a **bus**. Nic jiného neměním.

<img width="805" alt="Snímek obrazovky 2568-05-28 v 12 02 16" src="https://github.com/user-attachments/assets/dbc41c27-7621-433c-94ff-3e9cfe25d975" />


7. Kliknu na **Execute** a zkopíruji odkaz.
<img width="792" alt="Snímek obrazovky 2568-05-28 v 12 04 50" src="https://github.com/user-attachments/assets/31dd2cf4-5b54-46fb-a38e-86d5abca8582" />

8. Odkaz vložím do bloku `http request` do řádku **URL**.
<img width="470" alt="Snímek obrazovky 2568-05-28 v 12 04 59" src="https://github.com/user-attachments/assets/2ee955dd-e70b-4eff-bac0-1b662c86138d" />

9. Ve stejném bloku níže založím nový **header** a v kolonce nad změním na **JSON object**.  
   Do prvního pole headers zadám `X-Access-Token` a do druhého pole vygenerovaný token.
<img width="470" alt="Snímek obrazovky 2568-05-28 v 12 04 59" src="https://github.com/user-attachments/assets/a9c75fa5-63dc-4bbf-9466-51c1830bdbb2" />

10. Za blok `http` zapojím blok `function` a vložím tento kód:

    ```javascript
    var count = 0;
    for (var i = 0; i < msg.payload.features.length; i++) {
        count += msg.payload.features[i].properties.delay;
    }
    var prumer = count / msg.payload.features.length;
    msg.payload = prumer;
    return msg;
    ```
<img width="410" alt="Snímek obrazovky 2568-05-28 v 12 05 14" src="https://github.com/user-attachments/assets/482a792c-89d5-47a0-a101-be472222c3de" />

11. **Vysvětlení kódu:**
    - `var` znamená „vytvoř novou proměnnou“.
    - `for` znamená opakuj něco víckrát – cyklus.
    - `msg.payload` znamená hlavní obsah zprávy v Node-RED.
    - `return msg` znamená: pošli zprávu dál do dalšího bloku.

12. Jako poslední blok za `function` zapojím `debug`.
<img width="486" alt="Snímek obrazovky 2568-05-28 v 12 05 21" src="https://github.com/user-attachments/assets/5b7a6b98-26f9-4a68-8d8b-e98df1b4a420" />

13. Pokud chci mít kontrolu nad tím, jaká data přichází z Golemia, můžu vložit ještě jeden `debug` za `http request`.
<img width="357" alt="Snímek obrazovky 2568-05-28 v 12 05 41" src="https://github.com/user-attachments/assets/515f13fe-f6aa-483e-88db-23fb09bf2fca" />

14. Dám vpravo nahoře **Deploy**.

15. Kliknu na tlačítko u bloku `timestamp` a zkontroluju data vpravo v nabídce `debug`.

---

**A máme hotovo!**


Zobrazit více řádků
