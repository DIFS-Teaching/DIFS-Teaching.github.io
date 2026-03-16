<!-- .slide: class="section" -->

<header>
  <h1>Integrita a konzistence</h1>
</header>

---

# Databázová integrita
- Databáze vyhovuje zadaným pravidlům – **_integritním omezením (IO)_**. Tato integritní omezení bývají nejčastěji součástí definice databáze  a za jejich splnění zodpovídá **systém řízení báze dat (SŘBD)**
- Mohou být zadána výrazem (_deklarativně_) nebo programem (_procedurálně_)
- Integritní omezení se mohou týkat _jednotlivých hodnot_ vkládaných do polí databáze (například známka z předmětu musí být v rozsahu 1 až 5) 

---

# Databázová integrita
- Může jít o podmínku na _kombinaci hodnot_ v některých polích jednoho záznamu (například datum narození nesmí být pozdější než datum úmrtí). 
- Může se týkat _i celé množiny záznamů daného typu_ 
- Může jít o požadavek na _unikátnost hodnot daného pole či kombinace polí_ v rámci celé množiny záznamů daného typu, které se v databázi vyskytují (například číslo průkazu v záznamech o osobách).

---

# Integrita datovým typem
- _Datový typ_ je množina hodnot spolu s operacemi, které je možné nad těmito hodnotami provádět.
- Je vlastností jisté části modelu (proměnné, části jiného datového typu apod.) a _omezuje_ její použití (jde vlastně o _integritní omezení_ části modelu). Omezuje je tak, že tato část modelu může:
	- _nabývat pouze jisté množiny hodnot_ a
	- _může s ní být prováděna pouze jistá omezená množina operací_.
- Výhodou zavedení datového typu pro jistou část modelu je zejména možnost kontrolovat (a to nejčastěji předem), zda se s touto částí zachází korektně (zda ukládaná hodnota je správná a použitá operace správně použita). 

---
<!-- .slide: class="section" -->

<header>
  <h1>Integrita v relačních databázích</h1>
</header>

---

# Primární klíč
- Pole nebo kombinace polí, jednoznačně identifikující každý záznam v relaci. Žádné pole, které je součástí primárního klíče, nesmí obsahovat  nedefinovanou hodnotu. Každá tabulka má mít definovaný právě jeden primární klíč (_entitní integrita_).
- _Primární klíč_ má dvě základní vlastnosti: _jedinečnost_ v rámci tabulky a _definovanou hodnotu_.

---

# Primární klíč
- Databázový systém by měl být navržen a udržován tak, aby se primární klíč založeného záznamu nikdy nemusel měnit.
- Typickým příkladem primárního klíče je katalogové číslo u výrobků apod. Pokud u záznamu neexistuje žádný přirozený primární klíč, nebo je jeho použití problematické (změny, GDPR, apod.), používá se obvykle primární klíč, které záznamu přidělí SŘBD.

---

# Referenční integrita
- Častou v relačních databázích je tzv. _referenční integrita_. 
- Jedná se o požadavek, aby pro pole záznamu, jež má obsahovat odkaz na jiný záznam někde v databázi, takový odkazovaný záznam skutečně existoval, tedy aby takový odkaz nevedl _do prázdna_ a nejednalo se o tzv. _databázového sirotka_.
- Další integritní omezení lze definovat za pomocí tzv. _triggerů_. Jde o komplexnější (programově definované) definice kontrol, jež se budou provádět při každém pokusu o zápis záznamu do databáze.

---

# Referenční integrita
- Referenční integrita se definuje _cizím klíčem_, a to pro dvojici tabulek nebo nad jednou tabulkou, která obsahuje na sobě závislá data (například stromové struktury).
- Tabulka, v níž je pravidlo uvedeno, se nazývá podřízená tabulka (používá se také anglický termín _slave_). Tabulka, jejíž jméno je v omezení uvedeno, je nadřízená tabulka (_master_).

---

# Konzistence
- DB musí splňovat všechna _integritní omezení_ (IO)
- Udržování _interní konzistence_ (redundantních, vícenásobně uložených/replikovaných dat v distribuovaných systémech)
	- Máme více lokálních kopií dat (replikace)
	- Jak zajistíme, že jsou kopie vzájemně konzistentní?
- Dodržování _pravidel daných modelovaným systémem_

---

# Konzistence replikovaných dat
- Data-centrické modely
	- Několik procesů, jedna skupina dat – distribuovaný výpočet
	- Může být náročná na výměnu dat (objem zpráv)
	- Sekvenční konzistence – výsledek stejný, jako sekvenční provedení operací
- Klient-centrické modely
	- Jeden proces, několik skupin dat
	- Např. eventual consistency

---
<!-- .slide: class="section" -->

<header>
  <h1>Transakce</h1>
</header>

---

# Motivační otázky vzniku transakcí
- Co se stane, pokud dojde k poruše během práce s důležitými zdroji dat?
- Které operace prováděné nad daty systém stihl před poruchou skutečně provést a které ne? 
- Co se stane, když více uživatelů současně bude modifikovat tentýž údaj?
- Budou údaje v databázi stále smysluplné ?
- Hledáním odpovědí a jejich aplikací při zajištění spolehlivosti se zabývají **_transakční modely_** a celý obor **_transakčního zpracování_**.

---

# Pojem transakce
- **_Transakce_** představuje jednotku práce vykonávanou **_souvislým a bezpečným způsobem nezávisle na jiných transakcích_**.
	- *Databázové transakce* -- omezeno pouze na DB vrstvu (zajišťuje DB server)
	- *Business transakce* -- jednotka business logiky, nutno řešit na business vrstvě
		- Podpora na pokročilejších platformách pro implementaci IS, např. Java (ne PHP, Python)
- Transakce má dva základní účely:

---

# Pojem transakce
1. Poskytnout bezpečnou jednotku práce, která dovoluje správné **_zotavení z poruch_** a udržuje systém v konzistentním stavu i v případě poruchy systému, když je zastaveno provádění (úplně nebo částečně) a některé operace zůstávají nedokončené nebo v nejistém stavu 
2. Poskytnout **_izolaci souběžně prováděných operací_**. Pokud tato izolace není poskytnuta, výstupy jsou potenciálně chybové (souběh).

---

# Pojem transakce
- **_Skupina operací_** (akcí) prováděných jako celek (buď celá dávka nebo nic)
- Modelování stavu popisovaného výseku reálného světa
	- popis a provádění nerozlučných příkazů
	- první historické zmínky – 60. léta
	- důležitý pojem v oblasti databází
- **_Transakce_** je speciální druh programu, který je spouštěn v aplikaci **_OLTP_** (On Line Transaction Processing)

---

# Systém pro zpracování transakcí - TPS
- Systém (platforma, databázový systém) **_podporující provádění transakcí_** – transakční systém
- Zajišťuje speciální **_vlastnosti transakcí_** (atomičnost, nezávislost, trvanlivost)

- Angl. **_Transactional_** **_Processing_** **_System_** (zkratka **TPS**)

---

# Základní vlastnosti transakce
- Žádoucí vlastnosti transakcí jsou:
	- **_Atomičnost_** (**A**tomicity) – každá transakce je dokončena zcela nebo vůbec
	- **_Konzistence_** (**C**onsistence) – databázová konzistence (správná reflexe stavu reálného světa a dodržování omezujících pravidel pro hodnoty)
	- **_Izolovanost_** (**I**solation, **I**ndependence) – souběžné provádění má totožný efekt jako sekvenční
	- **_Trvanlivost_** (**D**urability) – odolnost proti ztrátě již dokončených změn
- V databázové praxi se pro tyto vlastnosti užívá akronym **_ACID_**.

---

# Kdo co zajišťuje
- Programátor je zodpovědný za vytváření konzistentních transakcí.  TPS považuje
	- **_konzistenci_** za zajištěnou programátorem (případně částečně systémem pro kontrolu integritních omezení)
- a zaopatřuje 
	- **_atomičnost_**, 
	- **_izolovanost_** a 
	- **_trvanlivost_**, 
- což jsou vlastnosti nutné pro zajištění **_souběžného spouštění konzistentních transakcí_** a případného **_zotavení z chyb či poruch_**.

---

# Transakce v business vrstvě IS
- Jednotlivé business operace obvykle představují elementární transakce
	- Podpora v některých SW frameworcích, např. Java EE
	- Např. převod zboží mezi sklady
- Někdy je nutno zajistit vlastnosti transakce pro skupinu transakcí
	- Např. kino: výběr vstupenky – výběr místa – platba 
	- Nutno zajistit na aplikační úrovni
	- Vede na hierarchické transakce
