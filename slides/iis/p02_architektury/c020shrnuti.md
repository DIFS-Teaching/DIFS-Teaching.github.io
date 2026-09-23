<!-- .slide: class="section" -->

<header>
	<h1>Návrh a implementace informačních systémů</h1>
	<p>Shrnutí</p>
</header>

---

# Model
- Stav modelu je uchováván v databázi podle zvoleného datového modelu, např.:
	- _relační model_ (nejčastěji),
	- dokumentový, grafový a další modely (NoSQL),
	- objektový model, případně jinak.

---

# Databáze
- Databáze pro modelování stavu není podmínkou, specializované IS např. pro řízení výroby v reálném čase používají i jiné typy uchování dat, nicméně databáze jako sídlo stavu modelu je nejčastější.
- Realizace databázového modelu je technologickou a provozní otázkou a může být např.:
	- **monolitický** (lokalizovaný na jediném místě, s jednou databází),
	- **distribuovaný** (s více lokálními databázemi, zde pak vznikají problémy s konzistencí)

---

# Procesy
- Modelovacím prostředím procesů modelu je nejčastěji nějaký univerzální programovací jazyk kompilovaný nebo i interpretovaný. 
- Snahy o modelování formálnějšími prostředky jako jsou např. různé modifikace automatů, _Petriho sítě_ nebo dnes nejčastěji notace _BPMN_. Při modelování procesů se musíme zabývat zejména:
	- udržováním **konzistence** systému,
	- **paralelním během procesů** (vícenásobným přístupem) a vzájemným ovlivňováním a
	- **transakčním zpracováním**.

---

# Nezbytné znalosti technologie
- Chceme-li se tedy zabývat informačními systémy musíme se zabývat:
- Způsobem vytváření modelů, **modelovacími technikami** a to zejména:
	- konceptuálním modelováním jako výchozím prostředkem pro modelování dat (tj. definicí modelu stavu fyzického systému na jisté úrovni abstrakce), převodem konceptuálního modelu na model databázový,
	- modelováním procesů a tedy i
	- univerzálními modelovacími prostředky, jako je např. UML nebo BPMN.

---

# Nezbytné znalosti technologie
- **Databázovými systémy** a jejich použitím a to zejména:
	- různými typy databázových modelů a jejich univerzálním rozhraním a ovládáním
	- transakčním zpracováním a pojmem transakce,
	- konzistencí dat
- **Modelováním procesů** a jejich případnou formalizací a to zejména:
	- programovacími jazyky vhodnými pro definici procesů,
	- formálními metodami definice procesů a workflow systémy,
	- souvislosti procesů s transakcemi a integritou,
	- metodami spouštění procesů.
- **Bezpečností** – autentizace, autorizace, ochrana osobních údajů (GDPR).

---

# Nezbytné znalosti technologie
- **Počítačovými sítěmi** a to zejména:
	- technologií klient-server a vytváření klientské a serverové části informačního systému
	- webovými službami a API (REST)
- **Vizualizací dat** a to zejména:
	- hypertextovou prezentací v HTML a pokročilejšími technikami (skripty, DOM),
	- prezentací pro dolování dat, OLAP a business intelligence.
- Mnohé z těchto témat pokrývají jeden nebo více samostatných povinných nebo volitelných předmětů. Zde se zabýváme jejich základy, zopakováním, doplněním a zejména spoluprací při vytváření komplexního systému.

