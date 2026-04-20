# InkTime - Proiect 

InkTime este un prototip de ceas inteligent construit în jurul platformei SoC nRF52840. Dispozitivul dispune de un display color TFT, conectivitate Bluetooth Low Energy (BLE 5.0), senzor pentru detecția mișcării și utilizează un sistem de alimentare liniar, conceput special pentru a fi eficient în utilizarea cotidiană.

## 2. Tabel Componente (Bill Of Materials)

| Componentă / Rol | Format (Package) | Cod JLCPCB | Fișă Tehnică (Datasheet) |
|-----------|---------|-----------|-----------|
| **Microcontroler** (nRF52840-QIAA-R) | aQFN73 (7x7) | [C190794](https://jlcpcb.com/partdetail/Nordic_Semicon-NRF52840_QIAA_R/C190794) | [Datasheet](https://docs.nordicsemi.com/) |
| **Încărcător Baterie** (BQ25120YBGR) | DSBGA-9 | [C1682423](https://jlcpcb.com/partdetail/TexasInstruments-BQ25180YBGR/C3682423) | [Datasheet](https://www.ti.com/lit/ds/symlink/bq25180.pdf) |
| **Fuel Gauge** (MAX17048G+T10) | DFN-8 (2x2) | [C2682616](https://jlcpcb.com/partdetail/AnalogDevices-MAX17048G_T10/C2682616) | [Datasheet](https://www.analog.com/media/en/technical-documentation/data-sheets/MAX17048-MAX17049.pdf) |
| **Regulator Buck-Boost** (RT6160AWSC) | WLCSP-15 | [C7065276](https://jlcpcb.com/partdetail/Richtek_Tech-RT6160AWSC/C7065276) | [Datasheet](https://www.richtek.com/assets/product_file/RT6160A/DS6160A-05.pdf) |
| **Accelerometru** (BMA421) | LGA-12 (2x2) | [C5242966](https://jlcpcb.com/partdetail/Bosch_Sensortec-BMA421/C5242966) | [Datasheet](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bma421-ds004.pdf) |
| **Driver Haptic** (DRV2605LDGSR) | VSSOP-10 | [C527464](https://jlcpcb.com/partdetail/TexasInstruments-DRV2605LDGSR/C527464) | [Datasheet](https://www.ti.com/lit/ds/symlink/drv2605l.pdf) |
| **Antenă BLE** (2450AT18B100E) | SMD 3216 | [C5179427](https://jlcpcb.com/partdetail/Johanson_Technology-2450AT18B100E/C5179427) | [Datasheet](https://www.johansontechnology.com/datasheets/2450AT18B100/2450AT18B100.pdf) |
| **Conector FPC** (Molex 503480-2400) | 24-pin 0.5mm FPC | [C2857168](https://jlcpcb.com/partdetail/Molex-5034802400/C2857160) | [Datasheet](https://www.molex.com/en-us/products/part-detail/5034802400) |
| **Butoane** (EVP-AKB31A) | SMD tactil | [C2845028](https://jlcpcb.com/partdetail/Panasonic-EVP_AKE31A/C2845028) | [Datasheet](https://industrial.panasonic.com/cdbs/www-data/pdf/ATV0000/ATV0000CE3.pdf) |
| **Mufă USB-C** (KH-TYPE-C-16P) | 16-pin SMD | [C2765186](https://jlcpcb.com/partdetail/Kinghelm-KH_TYPE_C_16P/C2765186) | [Datasheet](https://datasheet.lcsc.com/lcsc/2012121836_Kinghelm-KH-TYPE-C-16P_C2765186.pdf) |
| **Protecție ESD USB** (USBLC6-2SC6Y) | SOT-23-6 | [C7519](https://jlcpcb.com/partdetail/Stmicroelectronics-USBLC6_2SC6Y/C7519) | [Datasheet](https://www.st.com/resource/en/datasheet/usblc6-2.pdf) |
| **Tranzistor PFET** (Si2301CDS) | SOT-23 | [C10487](https://jlcpcb.com/partdetail/Changjiang_Electronics_Tech_CJ-SI2301CDS/C10487) | [Datasheet](https://www.vishay.com/docs/68749/si2301cds.pdf) |
| **Motor Vibrații** (LCM102733605F) | Fire atașate | [C7528006](https://jlcpcb.com/partdetail/7528806-LCM1027B3605F/C7528806) | [Datasheet](https://datasheet.lcsc.com/lcsc/2310131633_LCM-LCM1027B3605F_C7528806.pdf) |

**Componente Pasive & Periferice:**
* Interfață Programare: Header Tag-Connect 6-pin (TC2030-IDC)
* Cristale Oscilatoare: 32 MHz (2016) și 32.768 kHz (3215)
* Module externe: Display E-Paper / TFT 1.54 inch (FPC 24-pini), Acumulator LiPo 250 mAh
* Inductoare: 0.47uH (2012), 10uH (0402)
* Rezistențe (0201): 2x 10k, 2x 5.1k
* Condensatoare: 4x 12pF (0201), 5x 100nF (0201), 5x 4.7uF (0402), 2x 22uF (0402), 12x 1uF (0402)

## 3. Funcționalitatea Modulelor Hardware

**Unitatea de Procesare și Conectivitatea**
Creierul întregului sistem este cipul nRF52840 (la 64 MHz). Acesta execută logica aplicației și susține comunicarea wireless prin stiva BLE 5.0, permițând legătura cu smartphone-ul pentru sincronizarea timpului și preluarea notificărilor.

**Magistrale și Interfețe**
- **SPI (Doar transmisie):** Alocată exclusiv pentru display-ul TFT. Oferă o lățime de bandă mare, vitală pentru un framerate ridicat și tranziții fluide pe un ecran color.
- **I2C (400 kHz):** Prin intermediul acestei magistrale comunică senzorul inerțial (IMU) LSM6DS3TR-C. Folosirea I2C economisește pini valoroși și ușurează citirea datelor de accelerație.
- **PWM:** Comandă un tranzistor de tip N-MOSFET. Acesta joacă rolul de comutator de putere pentru motorul haptic (shaker-ul BST-BMV080), făcând posibilă generarea unor vibrații cu intensitate variabilă.

**Managementul Energiei (Power System)**
Pentru acest dispozitiv am implementat o arhitectură de alimentare liniară, punând accent pe fiabilitate și simplitate. Modulul BQ24040 primește 5V de la mufa USB-C și încarcă în condiții de siguranță bateria Li-Po de 250mAh (la un curent de 100mA). Mai departe, tensiunea variabilă a bateriei (3.0V - 4.2V) este coborâtă și stabilizată strict la 3.3V cu ajutorul unui regulator LDO (AP2112K). Acest LDO alimentează toată placa și a fost integrat datorită costului scăzut și a lipsei zgomotului electric la curenți mai mici de 600mA.

**Analiza Consumului de Energie**
Ecranele TFT, spre deosebire de cele e-paper, au nevoie de iluminare (backlight) continuă pentru a fi lizibile.
- *Consum în sarcină (Activ):* Aprox. 25 mA (TFT aprins la o luminozitate medie + procesorul activ).
- *Consum în repaus (Stand-by):* Aprox. 0.8 mA (Ecranul este oprit, MCU intră în modul sleep, funcția de BLE advertising este activă, iar IMU-ul așteaptă o mișcare pentru a trezi ceasul).
- *Estimare Autonomie:* Presupunând un scenariu zilnic cu 25 de treziri ale ecranului (a câte 5 secunde) și notificări haptice ocazionale, consumul se ponderează la o medie de 1.1 mA/h. În aceste condiții, acumulatorul de 250mAh asigură o durată de viață teoretică de 8 până la 9 zile de funcționare continuă.

## 4. Maparea Pinilor pentru nRF52840

Pinii au fost distribuiți având ca scop principal optimizarea traseelor de cupru pe placă (routing) și izolarea semnalelor rapide.

| Pin nRF | Periferic | Justificare / Rol Tehnic |
|---|---|---|
| **P0.29** | TFT SCK | Semnal de ceas rapid. Rutat special pe marginea PCB-ului către pamblica ecranului. |
| **P0.31** | TFT MOSI | Pin de date SPI. Tratat în paralel cu SCK pentru a evita degradarea semnalului grafic. |
| **P0.02** | TFT CS | Chip Select (activează display-ul pe magistrală). |
| **P0.26** | TFT DC | Data/Command. Necesar în mod obligatoriu pentru interpretarea comenzilor de către driverul ST7789. |
| **P0.27** | I2C SCL | Semnalul de clock pentru I2C, utilizat exclusiv de IMU. |
| **P0.28** | I2C SDA | Date I2C. Grupate special la distanță de liniile SPI pentru a elimina posibilele interferențe (crosstalk). |
| **P1.11** | Shaker PWM | Portul 1 a fost alocat pentru comenzi mecanice și de forță. Controlează grila tranzistorului de pe motoraș. |
| **P1.04** | Buton 1 (Sus) | GPIO setat ca intrare cu rezistență de pull-up internă. Folosit și pentru a trezi sistemul din hibernare. |
| **P1.05** | Buton 2 (OK) | Intrare digitală. Toți pinii butoanelor sunt adiacenți pentru a face rutarea pe margine extrem de scurtă. |
| **P1.06** | Buton 3 (Jos) | Intrare digitală pentru navigarea interfeței grafice. |
| **VBUS** | 5V USB | Pin hardware nativ al procesorului, capabil să citească prezența curentului de la încărcător. |
| **SWDIO** | Programare | Pin de date folosit la prima "flash-uire" a codului prin SWD / J-Link. |
| **SWDCLK**| Programare | Semnalul de ceas pentru protocolul de depanare SWD. |
