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

7. Kliknu na **Execute** a zkopíruji odkaz.

8. Odkaz vložím do bloku `http request` do řádku **URL**.

9. Ve stejném bloku níže založím nový **header** a v kolonce nad změním na **JSON object**.  
   Do prvního pole headers zadám `X-Access-Token` a do druhého pole vygenerovaný token.

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

11. **Vysvětlení kódu:**
    - `var` znamená „vytvoř novou proměnnou“.
    - `for` znamená opakuj něco víckrát – cyklus.
    - `msg.payload` znamená hlavní obsah zprávy v Node-RED.
    - `return msg` znamená: pošli zprávu dál do dalšího bloku.

12. Jako poslední blok za `function` zapojím `debug`.

13. Pokud chci mít kontrolu nad tím, jaká data přichází z Golemia, můžu vložit ještě jeden `debug` za `http request`.

14. Dám vpravo nahoře **Deploy**.

15. Kliknu na tlačítko u bloku `timestamp` a zkontroluju data vpravo v nabídce `debug`.

---

**A máme hotovo!**


Zobrazit více řádků
