12.MATURITNÍ OTÁZKA

Zadání: 12. Praktické krimpování konektorů, zapojení keystonů. Teorie sériové komunikace, sběrnice CIB. a. Co je to komunikační protokol? A jaké znáte? b. Co je to komunikační protokol? TCP, UDP? c. Co je to sériová komunikace? d. Popište komunikační standard Modbus e. Co je rack a patchpanel? f. Kabeláž, PoE, dělení kroucené dvojlinky

<img width="259" alt="Snímek obrazovky 2568-05-28 v 14 01 33" src="https://github.com/user-attachments/assets/9a8f4d96-08d8-4cd8-adac-3c9173296ee6" />


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

                    		















