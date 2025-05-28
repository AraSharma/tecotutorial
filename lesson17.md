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
<img width="687" alt="Snímek obrazovky 2568-05-28 v 12 09 39" src="https://github.com/user-attachments/assets/6c80629a-1f14-48a9-8f0b-5c89df09a8e4" />


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
<img width="520" alt="Snímek obrazovky 2568-05-28 v 12 10 22" src="https://github.com/user-attachments/assets/536710ba-dfbf-4d2b-8f89-5f5eeb54b235" />

11. **Vysvětlení kódu:**
    - `var` znamená „vytvoř novou proměnnou“.
    - `for` znamená opakuj něco víckrát – cyklus.
    - `msg.payload` znamená hlavní obsah zprávy v Node-RED.
    - `return msg` znamená: pošli zprávu dál do dalšího bloku.

12. Jako poslední blok za `function` zapojím `debug`.
<img width="674" alt="Snímek obrazovky 2568-05-28 v 12 11 32" src="https://github.com/user-attachments/assets/24556b1a-9bba-47b2-9430-60277b94b90d" />

13. Pokud chci mít kontrolu nad tím, jaká data přichází z Golemia, můžu vložit ještě jeden `debug` za `http request`.


14. Dám vpravo nahoře **Deploy**.

15. Kliknu na tlačítko u bloku `timestamp` a zkontroluju data vpravo v nabídce `debug`.
<img width="366" alt="Snímek obrazovky 2568-05-28 v 12 12 45" src="https://github.com/user-attachments/assets/48b41e8b-b462-4626-b8bc-db5d2204f8dc" />

---

**A máme hotovo!**


Zobrazit více řádků
