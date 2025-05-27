
# 💡 10 - TECO CFC programování & LED technologie

## 🎯 Zadání

10. TECO, praktické programování v jazyce CFC. LED osvětlení. Konfigurace ovládání LED svítidel, automatické ovládání. Teorie technologie LED svítidel. 

## 🧪 Úkol č.1
Po stisknutí levé horní části tlačítka na prvním ovladači (Logus) se část LED panelu (LED1) rozsvítí na 100%. LED panel zhasnete podržením levého spodního tlačítka na prvním ovladači (Logus). 

### Příprava mosaic: 

1. vytvořit novou skupinu projektů   
2. vytvořit nový projekt   
3. nastavit stejnou IP adresu na PC jako je v kufříku   
4. připojit se přes ethernet v Mosaicu   
5. stáhnout konfiguraci kufříku (obrázek ozubené kolečko oranžova šipka)    
6. klikni na průzkumník knihoven (ikona knihy s lupou)    
7. přidej knihovnu iControlLib_V35_20230620 (ikona knihy s plusem)   

### Postup:

1. z knihovny iControlLib_V35_20230620 vyber funkční blok fb_iDimmerLED a přidej ho  
2. pojmenuj funkční blok dle své preference  
3. z C-DM-0006M-ULED vyber LED1 a zapoj do level na funkčním bloku  
4. z C-WS-0400R-Logus vyber CLICK_UP1 a zapoj do lightOn na funkčním bloku  
5. vyber PRESS_DOWN1 a zapoj do lightOff na funkčním bloku  
6. vlož proměnou ( ), pojmenuj podle své preference a zapoj do setLevel  

---

## 🧪 Úkol č.2
Po stisknutí pravého horního tlačítka na prvním ovladači (Logus) se druhá část LED panelu (LED2) postupným rozsvícením během 10s rozsvítí z 0% na 100% (rampa).

1. z knihovny iControlLib_V35_20230620 vyber funkční blok fb_iDimmerLED a přidej ho stejně jako v úkolu č.1  
2. pojmenuj funkční blok dle své preference  
3. z C-DM-0006M-ULED vyber LED2 a zapoj do level na funkčním bloku  
4. z C-DM-0006M-ULED vyber ramp2 a zapoj do ramp na funkčním bloku  
5. z C-WS-0400R-Logus vyber CLICK_UP2 a zapoj do lightOn na funkčním bloku  
6. vyber DOWN2 a zapoj do lightOff na funkčním bloku  
7. vlož proměnou ( ), pojmenuj podle své preference a zapoj do setLevel  
8. vlož další proměnou, pojmenuj, nastav na 10s a zapoj do setRamp  

---

## 📦 Celkový výsledek
<img width="446" alt="Snímek obrazovky 2568-05-28 v 0 17 56" src="https://github.com/user-attachments/assets/7b2ccee1-d77f-4bf6-8bd4-a36bff215a5f" />

