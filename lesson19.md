[lesson19.json](https://github.com/user-attachments/files/20485872/lesson19.json)19.MATURITNÍ OTÁZKA
Zadání: 19. Praktické cvičení v programu Node-Red – práce s Real-Time daty, tvorba dashboardu, uživatelský vstup, ošetření výjimek. Práce s jednorozměrnými a dvourozměrnými poli. 
Pokuste se sestavit řešení v programu Node-red, které umožní uživateli pomocí textového pole v dashboardu vložit číslo linky autobusu a na základě tohoto údaje se vypíše pomocí grafu typu gauge aktuální zpoždění prvního autobusu v poli na uvedené lince. Zároveň se pokuste ošetřit nodem možné výjimky. Autorizační klíč máte k dispozici na ploše počítače v textovém souboru. Nastavte datovou sadu na webové stránce https://api.golemio.cz/v2/pid/docs/openapi/ tak, aby do vašeho řešení v programu Node-red přicházela data o aktuální pozici autobusů včetně jejich zpoždění.
Přetáhnu na plochu blok text input
Ten otevřu a přidám novou skupinu, tu pojmenuju.
  -><img width="685" alt="Snímek obrazovky 2568-05-28 v 13 27 46" src="https://github.com/user-attachments/assets/3a512a4d-c1de-410a-9fe5-71983b202481" />

-> 
Za to zapojím http request
 <img width="377" alt="Snímek obrazovky 2568-05-28 v 13 28 46" src="https://github.com/user-attachments/assets/deb607c8-3553-4784-ab97-9b87a76d2f40" />

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

<img width="281" alt="Snímek obrazovky 2568-05-28 v 13 29 23" src="https://github.com/user-attachments/assets/f7e304bb-421b-459c-b02d-daef111f6367" />

Jako další zapojím dashboardu blok gauge a ten pojmenuji zpozdeni autobusu v sekundách a nastavím max na 360 sekund. V kolonce group vyberu možnost, kterou jsem založila na začátku v text inputu. Můžu i upravit barvy. 

Odešlu deploy

Následně otevřu pod debugem tuto šipku a kliknu na dashboard 
<img width="259" alt="Snímek obrazovky 2568-05-28 v 13 29 51" src="https://github.com/user-attachments/assets/928079cb-3276-482e-9e4e-af75bdcfc732" />

Potom otevřu tuto „odkazovou“ šipku a ta mě hodí na webovou stránku s grafem, kde můžu zkusit zadat číslo jakéhokoli autobusu, kter existuje a vyhodí mi to jeho aktuální zpoýdění v sekundách

[Uploading lesson19.json…][
    {
        "id": "ac9f4272dc6b8add",
        "type": "tab",
        "label": "Flow 3",
        "disabled": false,
        "info": "",
        "env": []
    },
    {
        "id": "309808afd3298f2b",
        "type": "ui_text_input",
        "z": "ac9f4272dc6b8add",
        "name": "",
        "label": "",
        "tooltip": "",
        "group": "ec13b9481446cce1",
        "order": 0,
        "width": 0,
        "height": 0,
        "passthru": true,
        "mode": "text",
        "delay": 300,
        "topic": "topic",
        "sendOnBlur": true,
        "className": "",
        "topicType": "msg",
        "x": 260,
        "y": 220,
        "wires": [
            [
                "6c6ab9d9180f8b53"
            ]
        ]
    },
    {
        "id": "6c6ab9d9180f8b53",
        "type": "http request",
        "z": "ac9f4272dc6b8add",
        "name": "",
        "method": "GET",
        "ret": "obj",
        "paytoqs": "ignore",
        "url": "https://api.golemio.cz/v2/public/vehiclepositions?boundingBox=50.123%2C14.243%2C50.017%2C14.573&routeShortName={{payload}}&routeShortName=X1&routeType=bus",
        "tls": "",
        "persist": false,
        "proxy": "",
        "insecureHTTPParser": false,
        "authType": "",
        "senderr": false,
        "headers": [
            {
                "keyType": "other",
                "keyValue": "X-Access-Token",
                "valueType": "other",
                "valueValue": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MjI3NiwiaWF0IjoxNzAxNjk1OTU1LCJleHAiOjExNzAxNjk1OTU1LCJpc3MiOiJnb2xlbWlvIiwianRpIjoiMWQ1M2UxMjctOGUzMy00N2M5LTk0ZDctZTE4MWU3NDk4MzNhIn0.fjaJKNu9myym0lWFHTTlG55bg_kyOwctu2Nt0SKCqBc"
            }
        ],
        "x": 410,
        "y": 220,
        "wires": [
            [
                "8590d4f995f08080"
            ]
        ]
    },
    {
        "id": "8590d4f995f08080",
        "type": "function",
        "z": "ac9f4272dc6b8add",
        "name": "function 2",
        "func": "\nif (msg.payload.features != undefined) {\n    msg.payload = msg.payload.features[0].properties.delay;\n} else {\n    msg.payload = \"NEEXISTUJE!\";\n}\nreturn msg;\n",
        "outputs": 1,
        "timeout": 0,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 580,
        "y": 220,
        "wires": [
            [
                "80dd6a648dd8024f"
            ]
        ]
    },
    {
        "id": "80dd6a648dd8024f",
        "type": "ui_gauge",
        "z": "ac9f4272dc6b8add",
        "name": "",
        "group": "ec13b9481446cce1",
        "order": 1,
        "width": 0,
        "height": 0,
        "gtype": "gage",
        "title": "gauge",
        "label": "units",
        "format": "{{value}}",
        "min": 0,
        "max": "360",
        "colors": [
            "#00b500",
            "#e6e600",
            "#ca3838"
        ],
        "seg1": "",
        "seg2": "",
        "diff": false,
        "className": "",
        "x": 750,
        "y": 220,
        "wires": []
    },
    {
        "id": "ec13b9481446cce1",
        "type": "ui_group",
        "name": "Default",
        "tab": "f936bad53a63c0e9",
        "order": 1,
        "disp": true,
        "width": 6,
        "collapse": false,
        "className": ""
    },
    {
        "id": "f936bad53a63c0e9",
        "type": "ui_tab",
        "name": "zpzdeni",
        "icon": "dashboard",
        "disabled": false,
        "hidden": false
    }
]()

A máme hotovo!
