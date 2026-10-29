---
style: page
title: Datu baseak
---
### 1. E/R sortu:
---
Erronka honetan, streaming-plataforma baten datu-basea diseinatu dugu, erabiltzaileak, profilak, edukiak eta harpidetzak modu antolatuan kudeatzeko. Horretarako, entitate-erlazio diagrama (ER diagrama) sortu dugu, sistemaren elementu nagusiak eta haien arteko erlazioak irudikatzeko.

Lehenik eta behin, erabiltzaileak eta perfilak definitu ditugu. Erabiltzaile bakoitzak bere datu pertsonalak ditu, hala nola NAN, helbide elektronikoa, izena, abizena eta pasahitza. Horrez gain, perfilak sortu eta kudea daitezke, perfil bakoitzak bere identifikatzailea du eta mota desberdineko izan ahal da (Pertsonala, Familiarra edo Infantila)

Bestalde, plataformak eskaintzen dituen edukiak ere definitu ditugu. Eduki bakoitzak identifikatzaile bat, izenburua, adin-sailkapena, deskribapena eta urtea ditu. Edukiak hiru motatan banatzen dira: pelikulak, dokumentalak eta serieak. Mota bakoitzak (Pelikulak, Doku, Seriea) bere ezaugarri espezifikoak ditu. Adibidez, pelikulak; zuzendariaren izena eta pelikularen iraupena minututan eskatzen du, dokumentalak aldiz; iraupena minututan eta gaia (Natura eta animaliak, Kirolak, Gizartea eta kultura, Musika eta artea, Biografiak, Krimenak eta ikerketak). Serieak, berriz, denboraldietan banatzen dira, denboraldi bakoitzak zenbakietan identifikatzen da eta denboraldi bakoitzak hainbat kapitulu izan ditzake.

Horrez gain, erabiltzaileek harpidetza-plan desberdinak izan ditzakete. Bi plan mota definitu ditugu; estandarra eta premiuma. Plan bakoitzak bere ezaugarriak ditu, eta harpidetzen bidez erabiltzaileek plataformako zerbitzuetara sarbidea dute. Harpidetzek hasiera- eta amaiera-datak dituzte, eta horien bidez harpidetzaren iraupena kontrola daiteke.

Azkenik, entitateen arteko erlazioak eta kardinalitateak zehaztu ditugu, sistema osoaren funtzionamendua behar bezala irudikatzeko. Horrela, erabiltzaileen, profilen, edukien eta harpidetzen arteko loturak argi geratzen dira, eta datu-basearen egitura modu logiko eta antolatuan definitzen da.

Ondorioz, ER diagramaren helburua streaming-plataforma baten informazioa modu eraginkorrean antolatzea da, datuak behar bezala gordetzeko, erlazionatzeko eta etorkizunean kontsultatu eta kudeatu ahal izateko.

  ![digrama](img/db/1.png)

### 2. Modu erlazionala egin:
---
ER diagrama egin ondoren, zerrenda erlazionala sortu dugu, entitateak eta haien arteko erlazioak taula bihurtuz, atributuak zehaztuz eta gako primarioak (PK) eta gako arrotzak (FK) identifikatuz.

![eredu erlazioanala](img/db/ereduer.png)


### 3. Datu basea normalizatu (1F-2F-3F):
---
Ondoren, datu-basearen normalizazioa landu dugu, hiru forma normalak aplikatuz. Lehen forma normalean (1F), atributu bakoitzak balio bakarra izatea eta datuak behar bezala antolatuta egotea ziurtatu dugu. Bigarren forma normalean (2F), menpekotasun partzialak aztertu ditugu, atributu bakoitza gako primario osoaren menpe egon dadin. Azkenik, hirugarren forma normalean (3F), menpekotasun iragankorrak aztertu ditugu, datuen errepikapenak eta eguneratze-arazoak saihesteko.


#### HARPIDETZA

**Erlazioa:** `HARPIDETZA (ID_HARPIDETZA, Hasiera_data, Amaiera_data)`

- **1FN:** Bai. Ez dago errepikapenik; datuak atomikoak dira.
- **2FN:** Bai. Ez dago dependentzia partzialik.
- **3FN:** Bai. Ez dago dependentzia funtzional transitiborik (guztiak).

---

#### PLANA

**Hasierako erlazioa:** `PLANA (ID_PLANA, ID_HARPIDETZA, Mota)`

- **1FN:** Bai. Ez dago errepikapenik; datuak atomikoak dira.
- **2FN:** Ez. Dependentzia partziala dago.

| Gakoa | Mendeko atributuak |
|---|---|
| `ID_PLANA` | `Mota` |
| `ID_HARPIDETZA` | — |

Deskonposizioa:

- `PLANA (ID_PLANA, Mota)`
- `PLANA (ID_PLANA, ID_HARPIDETZA)`

- **3FN:** Bai. Ez dago dependentzia funtzional transitiborik (guztiak).

---

#### ERABILTZAILEA

**Hasierako erlazioa:** `ERABILTZAILEA (NAN, ID_PLANA, Izena, Abizena, Pasahitza)`

- **1FN:** Bai. Ez dago errepikapenik; datuak atomikoak dira.
- **2FN:** Ez. Dependentzia partziala dago.

| Gakoa | Mendeko atributuak |
|---|---|
| `NAN` | `Izena`, `Abizena`, `Pasahitza` |
| `ID_PLANA` | — |

Deskonposizioa (jatorrizko testuan adierazitakoa):

- `NAN (Izena, Abizena, Pasahitza)`
- `ERABILTZAILEA (EMAILA eta ID_PLANA)`

- **3FN:** Bai. Ez dago dependentzia funtzional transitiborik (guztiak).

---

#### PERFIL

**Hasierako erlazioa:** `PERFIL (ID_IZENA, NAN, Pertsonala, Familiarra, Infantila)`

- **1FN:** Bai. Ez dago errepikapenik; datuak atomikoak dira.
- **2FN:** Ez. Dependentzia partziala dago.

| Gakoa | Mendeko atributuak |
|---|---|
| `ID_IZENA` | `Pertsonala`, `Familiarra`, `Infantila` |
| `NAN` | — |

Deskonposizioa:

- `ID_IZENA (Pertsonala, Familiarra, Infantila)`
- `PERFIL (ID_IZENA eta NAN)`

- **3FN:** Bai. Ez dago dependentzia funtzional transitiborik (guztiak).

---

#### IKUSI

**Hasierako erlazioa:** `IKUSI (ID_IZENA, ID_EDUKIAK, Bistaratzea)`

- **1FN:** Bai. Ez dago errepikapenik; datuak atomikoak dira.
- **2FN:** Ez. Dependentzia partziala dago.

| Gakoa | Mendeko atributuak |
|---|---|
| `ID_IZENA` | — |
| `ID_EDUKIAK` | — |
| `IKUSI` | `Bistaratzea` |

Deskonposizioa:

- `IKUSI (ID_IZENA eta ID_EDUKIAK, Bistaratzea)`

- **3FN:** Bai. Ez dago dependentzia funtzional transitiborik (guztiak).

---

#### EDUKIAK

**Erlazioa:** `EDUKIAK (ID_EDUKIAK, Adin_sailkapena, Izenburua, Urtea, Deskribapena, Izenburua, Mota)`

- **1FN:** Bai. Ez dago errepikapenik; datuak atomikoak dira.
- **2FN:** Bai. Ez dago dependentzia partzialik.
- **3FN:** Bai. Ez dago dependentzia funtzional transitiborik (guztiak).

---

#### PELIKULAK

**Erlazioa:** `PELIKULAK (Zuzendaria, Iraupena_min)`

- **IDa:** EDUKIKO FK (`id`).
- **1FN:** Bai. Ez dago errepikapenik; datuak atomikoak dira.
- **2FN:** Bai. Ez dago dependentzia partzialik.
- **3FN:** Bai. Ez dago dependentzia funtzional transitiborik.

---

#### DOKU

**Erlazioa:** `DOKU (Gaia, Iraupena_min)`

- **IDa:** EDUKIKO FK (`id`).
- **1FN:** Bai. Ez dago errepikapenik; datuak atomikoak dira.
- **2FN:** Bai. Ez dago dependentzia partzialik.
- **3FN:** Bai. Ez dago dependentzia funtzional transitiborik.

---

#### SERIEAK

- **IDa:** EDUKIKO FK (`id`).
- **1FN:** Bai. Ez dago errepikapenik; datuak atomikoak dira.
- **2FN:** Bai. Ez dago dependentzia partzialik.
- **3FN:** Bai. Ez dago dependentzia funtzional transitiborik.

---

#### DENBORALDIAK

**Hasierako erlazioa:** `DENBORALDIAK (ID_DENBORALDIA, ID_EDUKIAK, Zenbakia)`

- **1FN:** Bai. Ez dago errepikapenik; datuak atomikoak dira.
- **2FN:** Ez. Dependentzia partziala dago.

| Gakoa | Mendeko atributuak |
|---|---|
| `ID_DENBORALDIA` | `Zenbakia` |
| `ID_EDUKIAK` | — |

Deskonposizioa:

- `ID_DENBORALDIAK (Zenbakia)`
- `DENBORALDIAK (ID_DENBORALDIA, ID_EDUKIAK)`

- **3FN:** Bai. Ez dago dependentzia funtzional transitiborik (guztiak).

---

#### KAPITULUAK

**Hasierako erlazioa:** `KAPITULUAK (ID_KAPITULUA, ID_DENBORALDIA, Izena)`

- **1FN:** Bai. Ez dago errepikapenik; datuak atomikoak dira.
- **2FN:** Ez. Dependentzia partziala dago.

| Gakoa | Mendeko atributuak |
|---|---|
| `ID_KAPITULUA` | `Izena` |
| `ID_DENBORALDIA` | — |

Deskonposizioa:

- `ID_KAPITULUA (Izena)`
- `ID_DENBORALDIAK (ID_KAPITULUA, ID_DENBORALDIA)`

- **3FN:** Bai. Ez dago dependentzia funtzional transitiborik (guztiak).



### 4. Datu basea ACCESS-en implementatu:
---
Datu-basea sortzeko, Microsoft Access erabili da. Programa honen bidez, taulak sortu eta atributuak definitu dira, gako nagusiak eta kanpo-gakoak esleitu dira, eta taulen arteko erlazioak ezarri dira. Prozesu honen esker, datu-basearen egitura koherenteagoa eta eraginkorragoa lortu nahi izan dugu, informazioa modu egokian gordetzeko, erlazionatzeko, kontsultatzeko eta eguneratzeko. 



### 1. Taulak eta haien atributuak

#### 1.1. HARPIDETZA
- `ID_HARPIDETZA` — Gako nagusia.
- `Hasiera_data` — Harpidetzaren hasiera-data.
- `Amaiera_data` — Harpidetzaren amaiera-data.

#### 1.2. PLANA
- `ID_PLANA` — Gako nagusia.
- `Mota` — Plan mota.

#### 1.3. ERABILTZAILEA
- `NAN` — Gako nagusia.
- `Izena` — Erabiltzailearen izena.
- `Abizena` — Erabiltzailearen abizena.
- `Pasahitza` — Erabiltzailearen pasahitza.
- `Email-a` — Erabiltzailearen helbide elektronikoa.

#### 1.4. PERFIL
- `ID_PERFIL` — Gako nagusia.
- `Mota` — Profil mota.

#### 1.5. IKUSI
- `ID_IZENA` — Gako nagusia.
- `Bistaratzea` — Edukiaren bistaratzearekin lotutako atributua.

#### 1.6. EDUKIAK
- `ID_EDUKIAK` — Gako nagusia.
- `Adin_sailkapena` — Edukiaren adin-sailkapena.
- `Izenburua` — Edukiaren izenburua.
- `Urtea` — Edukia argitaratu zen urtea.
- `Deskribapena` — Edukiaren deskribapena.
- `Mota` — Eduki mota.

#### 1.7. PELIKULAK
- `ID_EDUKIAK` — Gako nagusia (heredatua).
- `Zuzendaria` — Filmaren zuzendaria.
- `Iraupena_min` — Filmaren iraupena minututan.

#### 1.8. DOKU
- `ID_EDUKIAK` — Gako nagusia (heredatua).
- `Gaia` — Dokumentalaren gaia.
- `Iraupena_min` — Dokumentalaren iraupena minututan.

#### 1.9. SERIEAK
- `ID_EDUKIAK` — Gako nagusia (heredatua).

#### 1.10. DENBORALDIAK
- `ID_DENBORALDIA` — Gako nagusia.
- `Zenbakia` — Denboraldiaren zenbakia.

#### 1.11. KAPITULUAK
- `ID_KAPITULUA` — Gako nagusia.
- `Izena` — Kapituluaren izena.

### 2. Taulen gako nagusiak (PK) eta kanpo-gakoak (FK)

- **Gako nagusia (PK):** taula bateko erregistro bakoitza modu bakarrean identifikatzeko erabiltzen da. Ezin du balio errepikaturik edo hutsik izan.
- **Kanpo-gakoa (FK):** beste taula bateko gako nagusi batekin lotura ezartzeko erabiltzen da. Horri esker, datu-baseko taulen arteko erlazioak sortzen dira.

| Taula | Gako nagusia (PK) | Kanpo-gakoa(k) (FK) |
|---|---|---|
| HARPIDETZA | `ID_HARPIDETZA` | Bat ere ez |
| PLANA | `ID_PLANA` | `ID_HARPIDETZA` |
| ERABILTZAILEA | `NAN` | `ID_PLANA` |
| PERFIL | `ID_PERFIL` | `NAN` |
| IKUSI | `ID_PERFIL` + `ID_EDUKIAK` | `ID_PERFIL`, `ID_EDUKIAK` |
| EDUKIAK | `ID_EDUKIAK` | Bat ere ez |
| PELIKULAK | `ID_EDUKIAK` | `ID_EDUKIAK` |
| DOKU | `ID_EDUKIAK` | `ID_EDUKIAK` |
| SERIEAK | `ID_EDUKIAK` | `ID_EDUKIAK` |
| DENBORALDIAK | `ID_DENBORALDIA` | `ID_EDUKIAK` |
| KAPITULUAK | `ID_KAPITULUA` | `ID_DENBORALDIA` |

### 3. Access-eko taulen atributuen propietateak

#### 3.1. HARPIDETZA taula

| Eremuaren izena | Datu mota | Propietateak |
|---|---|---|
| ID_HARPIDETZA | Autonumerazioa | — |
| Hasiera_data | Data/Ordua | Formatua: Fecha corta |
| Amaiera_data | Data/Ordua | Formatua: Fecha corta |

#### 3.2. PLANA taula

| Eremuaren izena | Datu mota | Propietateak |
|---|---|---|
| ID_PLANA | Autonumerazioa | — |
| ID_HARPIDETZA | Zenbakia | FK – HARPIDETZA taula |
| Mota | Testu laburra | Asistente para búsquedas (Estándar edo Premium) |

#### 3.3. ERABILTZAILEA taula

| Eremuaren izena | Datu mota | Propietateak |
|---|---|---|
| NAN | Testu laburra | Máscara de entrada: NIF (90000000>L;;_) |
| ID_PLANA | Zenbakia | FK – PLANA taula |
| Izena | Testu laburra | Tamaño del campo = 30 |
| Abizena | Testu laburra | Tamaño del campo = 30 |
| Pasahitza | Testu laburra | Regla de validación = `*[A-Z]*.*` (gutxienez letra larri bat edukitzeko) |
| Email-a | Testu laburra | Regla de validación = `*@*` (@ ikurra edukitzeko) |

#### 3.4. PERFIL taula

| Eremuaren izena | Datu mota | Propietateak |
|---|---|---|
| ID_Perfil | Autonumerazioa | — |
| NAN | Testu laburra | FK – ERABILTZAILEA taula |
| Mota | Testu laburra | Asistente para búsquedas (Estándar edo Premium) |

#### 3.5. IKUSI taula

| Eremuaren izena | Datu mota | Propietateak |
|---|---|---|
| ID_Perfil | Zenbakia | — |
| ID_EDUKIAK | Zenbakia | — |
| Bistaratzea | Sí/No | — |

#### 3.6. EDUKIAK taula

| Eremuaren izena | Datu mota | Propietateak |
|---|---|---|
| ID_EDUKIAK | Autonumerazioa | — |
| Adin_sailkapena | Zenbakia | Regla de validación = `>18` (+18 urtetik gorakoentzat) |
| Izenburua | Testu laburra | Regla de validación = `*[A-Z]*.*` (gutxienez letra larri bat edukitzeko) |
| Deskribapena | Testu luzea | Tamaño del campo = 50 |
| Urtea | Zenbakia | Máscara de entrada = `0000` (4 digitu) |
| Mota | Testu laburra | — |

#### 3.7. PELIKULAK taula

| Eremuaren izena | Datu mota | Propietateak |
|---|---|---|
| ID_EDUKIAK | Zenbakia | — |
| Zuzendaria | Testu laburra | Tamaño del campo = 30 |
| Iraupena_min | Zenbakia | Fecha/Hora = Máscara de entrada: Hora larga |

#### 3.8. DOKU taula

| Eremuaren izena | Datu mota | Propietateak |
|---|---|---|
| ID_EDUKIAK | Zenbakia | — |
| Gaia | Testu laburra | Asistente para búsquedas (Natura eta animaliak, Kirolak, Gizartea eta kultura, Musika eta artea, Biografiak, Krimenak eta ikerketak) |
| Iraupena_min | Zenbakia | Fecha/Hora = Máscara de entrada: Hora larga |

#### 3.9. SERIEAK taula

| Eremuaren izena | Datu mota | Propietateak |
|---|---|---|
| ID_EDUKIAK | Zenbakia | Seriea EDUKIAK taulako gako nagusiarekin lotzen du. |

#### 3.10. DENBORALDIAK taula

| Eremuaren izena | Datu mota | Propietateak |
|---|---|---|
| ID_DENBORALDIA | Autonumerazioa | — |
| ID_EDUKIAK | Zenbakia | — |
| Zenbakia | Zenbakia | Valor predeterminado = 1 (1etik hasteko) |

#### 3.11. KAPITULUAK taula

| Eremuaren izena | Datu mota | Propietateak |
|---|---|---|
| ID_KAPITULUA | Autonumerazioa | — |
| ID_DENBORALDIA | Zenbakia | — |
| Izena | Testu laburra | Tamaño del campo = 30 |
| Izena | Testu laburra | Regla de validación = `*[A-Z]*.*` (gutxienez letra larri bat edukitzeko) |



### 4. Taulen arteko erlazioak

- **1:1:** taula bateko erregistro bakoitza besteko erregistro bakar batekin lotzen da.
- **1:N:** taula bateko erregistro bat besteko hainbat erregistrotara lot daiteke.
- **N:M:** bi tauletako erregistroak elkarren artean hainbat aldiz lotu daitezke.

| Erlazionatutako taulak | Lotutako atributuak | Erlazio mota |
|---|---|---|
| HARPIDETZA – PLANA | `ID_HARPIDETZA` | 1:N |
| PLANA – ERABILTZAILEA | `ID_PLANA` | 1:N |
| ERABILTZAILEA – PERFIL | `NAN` | 1:N |
| PERFIL – IKUSI | `ID_Perfil` | 1:N |
| EDUKIAK – IKUSI | `ID_EDUKIAK` | 1:N |
| EDUKIAK – PELIKULAK | `ID_EDUKIAK` | 1:1 |
| EDUKIAK – DOKU | `ID_EDUKIAK` | 1:1 |
| EDUKIAK – SERIEAK | `ID_EDUKIAK` | 1:1 |
| SERIEAK – DENBORALDIAK | `ID_EDUKIAK` | 1:N |
| DENBORALDIAK – KAPITULUAK | `ID_DENBORALDIA` | 1:N |

![eredu erlazioanala](img/db/erlazioakac.png)

