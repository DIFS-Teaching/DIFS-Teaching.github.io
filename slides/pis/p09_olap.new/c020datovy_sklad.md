<!-- .slide: class="section" -->

<header>
	<h1>Datové sklady</h1>
	<p>Data Warehouses</p>
</header>

---

# Pojem datového skladu

- Podnikově strukturovaný depozitář **subjektově orientovaných, integrovaných, časově proměnlivých, historických dat** použitých ke získávání **znalostí** a podpoře rozhodování
- Technologie pro:
	- **extrakci a transformaci** zdrojových dat,
	- **uložení** (loading) a
	- **poskytování** dat pro analytické dotazy
- Typicky provozován **odděleně** od produkční (OLTP) databáze

---

# Proč nestačí produkční databáze?

- Navrženy pro jednoduché transakce (vkládání, mazání) – **OLTP**
- Výsledkem dotazů jsou detailní explicitní data bez agregací
- Data jsou typicky **decentralizovaná** – různé heterogenní DB na různých serverech
- **Nehomogenní struktura** – různé názvy atributů, datové typy, kódování
- Opakující se agregační dotazy **degradují výkon** produkčního stroje
- Produkční DB obvykle neuchovávají **historická data**

---

# Vlastnosti datového skladu

| Vlastnost | Produkční DB | Datový sklad |
|---|---|---|
| Uživatelé | běžný uživatel | management |
| Data | aktuální, detailní | historická, sloučená |
| Model | ER, aplikační | multidimenzionální |
| Pohled | lokální | agregovaný |
| Přístup | čtení/zápis, transakce | read-only, komplexní dotazy |

---

# Integrace dat

- Data z **různých zdrojů** se ukládají s jednotnou terminologií a jednotkami
- Zdroje: relační databáze, textové soubory, on-line transakce, externí zdroje
- Nutná **úprava, vyčištění a sjednocení** – integrace
	- ověření konzistence pojmenování proměnných, jejich struktury a jednotek

---

# Časová dimenze

- **Klíčový atribut** – lineární, uspořádaný, vhodný pro spojité grafy
- Časový horizont datového skladu je podstatně **delší** než u produkční DB
	- Produkční DB: pouze aktuální data
	- Datový sklad: historická perspektiva (typicky 5–10 let)
- Každá klíčová struktura datového skladu obsahuje čas (explicitně nebo implicitně)

---

# Neměnnost dat

- Data v datovém skladu se **nemění** – jsou fyzicky oddělena od produkčních dat
- Dva typy operací: **vkládání** dat a **čtení** dat
- Nepotřebuje se:
	- zpracování transakcí a zotavení,
	- mechanismy pro řízení souběžného přístupu
- Optimalizace a normalizace (pro konzistenci zápisu) ztrácí smysl

---

# Celkové schéma datového skladu

```
Produkční prostředí          Datový sklad         Uživatelé
┌─────────────────┐         ┌────────────┐        ┌────────┐
│  Produkční DB   │ ──ETL──▶│  Uložení   │──OLAP─▶│ Dotazy │
│  Interní data   │         │  dat       │        │ Zprávy │
│  Externí zdroje │         │  Metadata  │        │ Analýza│
└─────────────────┘         └────────────┘        └────────┘
     Extrakce → Transformace → Loading (ETL)
```

---

# Architektura datového skladu

- **Získání dat (ETL)**
	- zdrojová data + místo přípravy (staging area)
- **Uložení dat**
	- datový sklad + datové trhy (_data marts_) + metadata
- **Předávání výsledků**
	- OLAP servery, dotazovací nástroje, generátory zpráv, data mining

---

# Datové trhy (Data Marts)

- Dílčí podmnožiny datového skladu zaměřené na konkrétní oblast (marketing, finance, …)
- Data uložena a spravována jedním nebo více **OLAP servery**
- Přístupné různým koncovým nástrojům

---

# Předávání výsledků

- **Začínající uživatelé:** tiskové sestavy, jednoduché dotazy
- **Běžní uživatelé:** statistická analýza, různá zobrazení, předdefinované dotazy
- **Pokročilí uživatelé:** multidimenzionální analýza, vlastní OLAP dotazy, data mining
