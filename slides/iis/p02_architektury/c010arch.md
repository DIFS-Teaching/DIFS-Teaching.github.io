
# Architektury – uložení a zpracování dat
- Centrální informační systémy
- Lokální síť
- Klient-server
- Monolitické architektury
	- Třívrstvá architektura
	- Modulární monolit
- Distribuované informační systémy
	- Architektury založené na službách

---

# Centrální informační systémy
- Centrální počítač (_mainframe_) s databází a aplikacemi
- Aktivace aplikačních programů z terminálů (_pracovních stanic_)
- Z hlediska architektury není použita síťová komunikace (není klient)

![Centrální architektura](assets/klientserver1.svg) <!-- .element: style="width:1100px" -->
<!-- .element: style="text-align:center" -->

---

# Lokální síť
- Zavedení lokálního klienta (osobní počítač -- PC)
- Aplikace na PC, databáze na speciálním serveru v rámci lokální sítě

![File-server](assets/klientserver2.svg) <!-- .element: style="width:1100px" -->
<!-- .element: style="text-align:center" -->

---

# Lokální síť
- Není použita globální síť a standardní protokoly Internetu a TCP-IP
- Server pouze sdílí soubory (_file-server_), SŘBD i aplikace běží na každém PC
	- Po síti se přenášejí celé soubory databáze → pomalé přenosy, nízká bezpečnost, obtížné zajištění integrity
- Vstupuje otázka _izolovanosti transakcí_, tj. možnosti _víceuživatelského přístupu_

---

# Architektura klient-server (dvouvrstvá)
- Užity dva druhy oddělených výpočetních systémů **klient** a **server**.
- _Tloušťka_ klienta odpovídá jeho „inteligenci“

![Klient-server](assets/klientserver3.svg) <!-- .element: style="width:1100px" -->
<!-- .element: style="text-align:center" -->

---

# Architektura klient-server
- Na nižší úrovni použita síťová komunikace standardizovaná protokoly Internetu TCP/IP
- Chování klienta a serveru rovněž standardizováno
	- Server specializovaný pro databázové dotazy
	- Po síti se přenášejí pouze dotazy a výsledky
- Klient posílá přímo **SQL dotazy** protokolem databázového serveru (ovladače ODBC, JDBC, …), zpět dostává **serializovaná data** (výsledky)

---

# Třívrstvá architektura
- (_three-tier architecture_) 
- **Prezentační vrstva** – vizualizuje informace pro uživatele, většinou formou grafického uživatelského rozhraní, může kontrolovat zadávané vstupy, neobsahuje však zpracování dat
- **Aplikační vrstva** – jádro aplikace, logika a funkce, výpočty a zpracování dat
- **Datová vrstva** – nejčastěji databáze. Může zde být ale také (síťový) souborový systém, webová služba nebo jiná aplikace.

---

# Terminologická odbočka
- **Tier** – fyzická vrstva – jednotka nasazení (deployment)
	- Fyzické členění systému – klient, aplikační server, DB server
	- Tomu odpovídá volba technologií pro realizaci jednotlivých částí
- **Layer** – logická vrstva – jednotka organizace kódu
	- Obvykle řešena v rámci aplikační vrstvy
	- _Data layer_ – část řešící komunikaci s databází
	- _Business layer_ – část implementující logiku aplikace
	- _Presentation layer_ – komunikace s klientem

---

# Schéma třívrstvé architektury
<!-- .slide: class="normal centered fullspace" data-transition="slide-in fade-out" -->

![Třívrstvá architektura](assets/3tier1.svg) <!-- .element: style="height:750px;margin:0;" -->

<div class="fragment box shadow" style="position:absolute;left:1200px;top:840px;padding:10px;">
Database server<br/>
(PostgreSQL, MySQL, Oracle, ...)
</div>

<div class="fragment box shadow" style="position:absolute;left:1200px;top:240px;padding:10px;">
Web browser
</div>

<div class="fragment box shadow" style="position:absolute;left:1200px;top:540px;padding:10px;">
Application server<br/>
(PHP, Java, .NET, Node.js, Python, ...)
</div>

<div class="fragment box shadow" style="position:absolute;right:1200px;top:320px;padding:10px;">
HTTP<br/>
(přenos dat, serializace)
</div>

<div class="fragment box shadow" style="position:absolute;right:1200px;top:780px;padding:10px;">
SQL<br/>
</div>

---

# Schéma třívrstvé architektury (II)
<!-- .slide: class="normal centered fullspace" data-transition="fade-in slide-out" -->

![Třívrstvá architektura](assets/3tier2.svg) <!-- .element: style="height:750px;margin:0;" -->

<div class="fragment box shadow" style="position:absolute;left:1200px;top:540px;padding:10px;">
PHP, Java, .NET, ...<br/>
Různá rámcová řešení (framework)
</div>

<div class="fragment box shadow" style="position:absolute;left:1200px;top:240px;padding:10px;">
Tenčí nebo tlustší klient v prohlížeči
</div>

<div class="fragment box shadow" style="position:absolute;left:1200px;top:840px;padding:10px;">
Datový model (objektový, relační, ...)
</div>

---

# Dvojvrstvá ⨉ Třívrstvá architektura

- Základní rozdíl: Aplikační logika oddělená od prezentační
	- Klient nepřistupuje přímo k databázi: bezpečnost, škálovatelnost, logika na jednom místě
- Klientem je typicky standardní webový prohlížeč
	- Snazší nasazení
		- Není třeba nic instalovat na klientská zařízení
		- Centrální aktualizace
	- Lepší přístupnost
		- Klient není omezen na konkrétní zařízení nebo operační systém

---

# Distribuované architektury
- Monolitický systém (typické pro třívrstvou architekturu)
	- Vyvíjí se a nasazuje jako jeden celek
	- \+ snáze zvládnutelný vývoj, testování
	- \- obtížnější a pomalejší nasazování nových verzí, škálování jen jako celek
	- Kompromis: _modulární monolit_
- Distribuované architektury
	- Service-oriented architecture (SOA)
	- Microservices (mikroslužby)
	- Spíše řešeno v rámci Pokročilých informačních systémů

---

# Modulární monolit
- Nasazuje se jako jeden celek, uvnitř je rozdělen na **moduly** podle oblastí (objednávky, sklad, uživatelé, …)
- Moduly spolu komunikují jen přes **veřejné rozhraní**
	- Volání v rámci jednoho procesu, ne po síti
- Každý modul spravuje svá data (vlastní tabulky / schéma), ostatní moduly k nim nepřistupují přímo
- \+ jednoduché nasazení a transakce, přehledná struktura kódu
- \+ modul lze později vyčlenit do samostatné služby
- Podpora např. Spring Modulith, moduly a balíčky v aplikačních frameworcích

---

# Mikroslužby
- Aplikace je rozdělena na malé části
	- Vlastní databáze (nepřístupná vně)
	- Business logika
	- Aplikační rozhraní (síťové)
- Typicky malý tým vývojářů na každou část (_two-pizza team_, Amazon)
- Nasazují se odděleně
- \+ Technologická nezávislost, rychlé aktualizace
- \- Testovatelnost, režie komunikace, konzistence dat (distribuované transakce), riziko nekompatibility, řetězové selhání, …

---

# Monolit ⨉ modulární monolit ⨉ mikroslužby
<!-- .slide: class="normal centered fullspace" -->

![Srovnání monolitu, modulárního monolitu a mikroslužeb](assets/monolit-mikrosluzby.svg) <!-- .element: style="height:760px;margin-top:30px;" -->
