<!-- .slide: class="section" -->

<header>
	<h1>SPARQL</h1>
	<p>Dotazování nad grafem</p>
</header>

---

# SPARQL: hledání vzoru v grafu

- Dotaz je **graf s proměnnými**; hledá se, čím je lze nahradit
- Proměnná začíná `?`; každý řádek vzoru je jedna trojice

```sparql
SELECT ?mesto ?pocet WHERE {
  ?mesto  wdt:P31    wd:Q5153359 .   # ?mesto je obec v Česku
  ?mesto  wdt:P1082  ?pocet .        # ?mesto má počet obyvatel ?pocet
}
```

- Databáze najde všechna přiřazení, pro která vzor v grafu existuje
- Žádné tabulky, žádné JOINy -- spojení vzniká **opakováním proměnné**
- [query.wikidata.org](https://query.wikidata.org/#SELECT%20%3Fmesto%20%3Fpocet%20WHERE%20%7B%0A%20%20%3Fmesto%20%20wdt%3AP31%20%20%20%20wd%3AQ5153359%20.%20%20%20%23%20%3Fmesto%20je%20obec%20v%20%C4%8Cesku%0A%20%20%3Fmesto%20%20wdt%3AP1082%20%20%3Fpocet%20.%20%20%20%20%20%20%20%20%23%20%3Fmesto%20m%C3%A1%20po%C4%8Det%20obyvatel%20%3Fpocet%0A%7D)

---

# Kde to spustit

- Veřejné endpointy: [query.wikidata.org](https://query.wikidata.org) · [dbpedia.org/sparql](https://dbpedia.org/sparql) · [data.gov.cz/sparql](https://data.gov.cz/sparql) · [qlever.dev](https://qlever.dev/)
- Editor [YASGUI](https://yasgui.triply.cc/) -- zvýrazňování, našeptávání, export
- Z programu: HTTP GET/POST na endpoint, výsledek jako JSON nebo CSV

```python
import requests

r = requests.get("https://query.wikidata.org/sparql",
                 params={"query": open("dotaz.rq").read()},
                 headers={"Accept": "text/csv"})
open("obce.csv", "w").write(r.text)
```

- Vždy začínejte s `LIMIT` -- endpointy mají **timeout i rate limit**
- Na velký objem stáhnout dump a nahrát lokálně (Fuseki, Oxigraph, QLever)

Note:
Ten curl je záměrně tentýž tvar jako minulý týden u ARES a ČNB. Jediný rozdíl
je, že se neptám na soubor, ale na graf.

---

# Čtyři formy dotazu

<div class="small">

| Forma | Výsledek | K čemu v pipeline |
|---|---|---|
| `SELECT` | **tabulka (CSV, JSON)** | načtu do pandas a pracuji dál |
| `CONSTRUCT` | nový graf | transformace: cizí slovník na vlastní |
| `ASK` | `true` / `false` | kontrola kvality, test v CI |
| `DESCRIBE` | graf okolo zdroje | průzkum neznámých dat |

</div>

- **SPARQL UPDATE**: `INSERT DATA`, `DELETE WHERE`, `LOAD`

---

# Verze s názvem obce

- Filtr na počet obyvatel

```sparql
SELECT ?mesto ?nazev ?pocet WHERE {
  ?mesto  wdt:P31    wd:Q5153359 .   # ?mesto je obec v Česku
  ?mesto  wdt:P1448  ?nazev .        # ?nazev je oficiální název
  ?mesto  wdt:P1082  ?pocet .        # ?mesto má počet obyvatel ?pocet
  FILTER (?pocet > 100000)
}
```

- [query.wikidata.org](https://query.wikidata.org/#SELECT%20%3Fmesto%20%3Fnazev%20%3Fpocet%20WHERE%20%7B%0A%20%20%3Fmesto%20%20wdt%3AP31%20%20%20%20wd%3AQ5153359%20.%20%20%20%23%20%3Fmesto%20je%20obec%20v%20%C4%8Cesku%0A%20%20%3Fmesto%20%20wdt%3AP1448%20%20%3Fnazev%20.%20%20%20%20%20%20%20%20%23%20%3Fnazev%20je%20ofici%C3%A1ln%C3%AD%20n%C3%A1zev%0A%20%20%3Fmesto%20%20wdt%3AP1082%20%20%3Fpocet%20.%20%20%20%20%20%20%20%20%23%20%3Fmesto%20m%C3%A1%20po%C4%8Det%20obyvatel%20%3Fpocet%0A%20%20FILTER%20%28%3Fpocet%20%3E%20100000%29%0A%7D)

---

# Dotaz na DBPedia

```sparql
PREFIX dbprop: <http://dbpedia.org/property/>
PREFIX dbo: <http://dbpedia.org/ontology/>
SELECT DISTINCT ?country ?name ?curLabel ?cur
WHERE 
{  ?country rdf:type dbo:Country;
      dbprop:commonName ?name ;
      dbo:currency ?cur .
   ?cur rdfs:label ?curLabel .
   OPTIONAL {?country dbprop:yearEnd ?yearEnd}
   FILTER (!bound(?yearEnd) && lang(?curLabel) = "en")
}
```

- [https://dbpedia.org/sparql](https://dbpedia.org/sparql)
- [https://qlever.dev/dbpedia/](https://qlever.dev/dbpedia/)

---

# Dotaz data.gov.cz

- Rejstřík orgánů veřejné moci: ID datových schránek všech krajských úřadů

```sparql
PREFIX ovm: <https://slovník.gov.cz/legislativní/sbírka/111/2009/pojem/>
PREFIX rpp: <https://slovník.gov.cz/agendový/104/pojem/>

SELECT ?nazev ?ico ?schranka WHERE {
  ?z    rpp:zařazuje-do-kategorie/ovm:má-název-kategorie "Krajské úřady"@cs ;
        rpp:má-zařazený-subjekt  ?urad .
  ?urad ovm:má-název-orgánu-veřejné-moci ?nazev ;
        ovm:má-identifikační-číslo-osoby-orgánu-veřejné-moci ?ico ;
        ovm:má-datovou-schránku-orgánu-veřejné-moci/ovm:má-identifikátor-datové-schránky ?schranka .
}
ORDER BY ?nazev
```

- [data.gov.cz/sparql](https://data.gov.cz/sparql) -- 13 krajů, IRI včetně diakritiky

---

# Výsledek

<div class="small">

| nazev | ico | schranka |
|---|---|---|
| Jihomoravský kraj | 70888337 | x2pbqzq |
| Jihočeský kraj | 70890650 | kdib3rr |
| Karlovarský kraj | 70891168 | siqbxt2 |
| Kraj Vysočina | 70890749 | ksab3eu |
| Královéhradecký kraj | 70889546 | gcgbp3q |
| ... | ... | ... |

</div>

- `?z` je **pomocný uzel** -- zařazení do kategorie nese i datum, proto není vztah přímý
- `/` je **property path**: zkratka za průchod přes mezilehlý uzel
