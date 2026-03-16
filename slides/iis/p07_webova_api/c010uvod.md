# Webová API

- Na HTTP požadavek můžeme chápat jako na **volání vzdálené funkce na serveru**
	- Předáme jméno a parametry
	- Server vykoná nějaké operace
	- Vrátí výsledek (tradičně v HTML)
- Serializace umožňuje předávat strukturovaná data
	- V HTTP požadavku -- např. POST
	- V HTTP odpovědi -- v těle odpovědi (dokument)
- Nabízí se využití zejména XML a JSON

---

# Standardy pro webová API

- **XML-RPC** (1998)
	- Využívá pouze HTTP POST požadavky, přenáší se XML (`Content-Type: text/xml`)
	- Definuje jednoduchý formát dokumentů pro popis volání a odpovědi
		- Jméno volané funkce, jména parametrů
		- Výsledek volání (návratové hodnoty)
- **SOAP** (Simple Object Access Protocol, 2000) -- _**Web Services**_
	- Rozšíření formátu zpráv
	- WSDL (*Web Service Description Language*)
		- Umožňuje popsat a sdílet rozhraní služby v XML
		- Možnost automatického generování klienta na implementační platformě

---

# Příklad SOAP

```xml
<env:Envelope xmlns="...">
	<env:Header/>
	<env:Body>
		<m:jePrvocislo xmlns:m="urn:mojeURI">
			<cislo xsi:type="xs:long">1987</cislo>
		</m:jePrvocislo>
	</env:Body>
</env:Envelope>
```

```xml
<env:Envelope xmlns="...">
	<env:Body>
		<m:jePrvocisloResponse xmlns:m="urn:mojeURI">
			<return xsi:type="xsd:boolean">true</return>
		</m:jePrvocisloResponse>
	</env:Body>
</env:Envelope>
```

---

# REST

- XML-RPC a SOAP jsou (teoreticky) nezávislé na HTTP
- Vše se popisuje v XML dokumentech
	- Rozsáhlý standard, značná složitost dokumentů
	- Obtížná implementace
- REST -- Representational state transfer
	- Využijeme co nejvíce vlastnosti HTTP
	- Zjednodušíme přenášená data

---

# GraphQL

- https://graphql.org/ 
- Motivace: klient (klienti) potřebují v různých situacích různá data
	- Např. stránka „seznam osob“ vs. „detail osoby“
- REST endpoint vrací vždy stejnou strukturu
	- Redundance dat (nevyužijeme všechna data)
	- Více dotazů ((ne)efektivita, složitější logika klienta)
- Řešení GraphQL
	- Popis datového modelu API (na serveru, speciální jazyk)
	- Dotaz na API specifikuje požadovaný tvar odpovědi

---

# Dotazování GraphQL

- Jediné endpoint URL
- Odeslání přes GET
	- `http://myapi/graphql?query={me{name}}`
- Odeslání přes POST
	- Data `application/json` \
		`{"query": "{me{name}}"}`
	- Data `application/graphql` \
		`{me{name}}`
