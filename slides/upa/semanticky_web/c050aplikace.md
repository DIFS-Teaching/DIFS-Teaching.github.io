<!-- .slide: class="section" -->

<header>
	<h1>SPARQL v praxi</h1>
	<p>Co z toho reálně vytáhnu pro svoje data</p>
</header>

---

# SPARQL jako nástroj přípravy dat

- **Doplnit** -- k mým záznamům přidat, co o nich ví někdo jiný (*enrichment*)
- **Propojit** -- najít, že dvě různá IRI označují tutéž věc (*entity linking*)
- **Ověřit** -- zkontrolovat vlastní data proti referenčnímu zdroji

<p class="xfragment" style="font-size: 130%; text-align: center; margin-top: 0.8em;">Všechny dotazy na následujících slajdech jsou <strong>živé</strong>. <br>Zkuste je během přednášky.</p>

Note:
Záměrně to nejsou hračky. Každý z těch dotazů řeší úlohu, která se studentovi
v projektu opravdu vyskytne -- a jinak by na ni psal skript na dvě stě řádků.

---

# Doplnit: obohacení o to, co ví Wikidata

Mám nascrapovaný dataset se sloupcem IČO. Co se k němu dá dotáhnout?

```sparql
SELECT ?ico ?firmaLabel ?web ?zalozeno WHERE {
  VALUES ?ico { "00216305" "45274649" "00025593" }
  ?firma wdt:P4156 ?ico .                # IČO
  OPTIONAL { ?firma wdt:P856 ?web }      # web
  OPTIONAL { ?firma wdt:P571 ?zalozeno } # datum vzniku
  SERVICE wikibase:label { bd:serviceParam wikibase:language "cs,en". }
}
```

- `VALUES` definuje uvažované hodnoty `?ico`
- Kde se ptát?
  - [https://query.wikidata.org/](https://query.wikidata.org/)
  - [https://qlever.dev/wikidata](https://qlever.dev/wikidata)

---

# A rovnou i první problém

<div style="font-size: 88%">

<div class="small">

| ico | firmaLabel | web | zalozeno |
|---|---|---|---|
| 45274649 | ČEZ | cez.cz | 1992-01-01 |
| 00216305 | Vysoké učení technické v Brně | vut.cz | **1899-01-01** |
| 00216305 | Vysoké učení technické v Brně | vut.cz | **1956-01-01** |
| 00025593 | Český statistický úřad | csu.gov.cz | 1969-01-08 |

</div>

- Tři vstupní řádky, **čtyři výstupní** -- VUT má dvě tvrzení o datu vzniku
- Ani jedno není chyba: 1899 je založení české techniky, 1956 dnešní VUT; vícehodnotová vlastnost ⇒ **kartézský součin** ⇒ duplicity v exportu

<p class="xfragment" style="text-align: center; font-size: 125%;">Řešení: kvalifikátory, agregace, nebo vědomá volba jedné hodnoty.</p>

</div>

Note:
Nechat sál chvíli hádat, proč jsou tam čtyři řádky. Je to přesně ten typ tiché
chyby, která se v pipeline projeví až o tři kroky dál jako ``máme víc firem,
než jsme scrapovali''.

---

# Oficiální název přes P1448

```sparql
SELECT ?ico ?nazev ?web ?zalozeno WHERE {
  VALUES ?ico { "00216305" "45274649" "00025593" }
  ?firma wdt:P4156 ?ico .                # IČO
  ?firma wdt:P1448 ?nazev .              # Nazev
  OPTIONAL { ?firma wdt:P856 ?web }      # web
  OPTIONAL { ?firma wdt:P571 ?zalozeno } # datum vzniku
}
```

- Ještě větší exploze stavů

---

# Propojit: entity linking přes owl:sameAs

Mám IRI z DBpedie. Kde je totéž jinde?

```sparql
SELECT ?stejny WHERE { dbr:Brno owl:sameAs ?stejny }
```

<div class="col small">

```
wd:Q14960                ← Wikidata
sws.geonames.org/3078610 ← GeoNames
viaf.org/viaf/144231825  ← knihovny
d-nb.info/gnd/4008456-5  ← německá NK
yago-knowledge.org/Brno  ← YAGO
de.dbpedia.org/Brünn     ← DBpedia (de)
```

- [https://dbpedia.org/sparql](https://dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fdbpedia.org&query=SELECT+%3Fstejny+WHERE+%7B+dbr%3ABrno+owl%3AsameAs+%3Fstejny+%7D&format=text%2Fhtml&timeout=30000&signal_void=on&signal_unconnected=on)

</div>
<div class="col small">

- Record linkage, který za vás **už někdo udělal a publikoval**
- Ve výsledku je ale i `wd:Q850531` -- což je **okres Brno-město**, ne město

</div>

Note:
Endpoint: dbpedia.org/sparql. Tohle je ta praktická výhrada k owl:sameAs
ze slajdu o OWL -- formálně to znamená ``totožné ve všech ohledech'',
a přesto tam ta chyba je. Když si takový odkaz slepě importujete,
zdědíte ji i vy.

---

# Propojit: klíč do státních registrů

<div style="font-size: 88%">

```sparql
SELECT ?obecLabel ?ruian ?obyvatel ?sour WHERE {
  ?obec wdt:P31   wd:Q5153359 ;   # je obec v Česku
        wdt:P7606 ?ruian ;        # kód obce v RÚIAN
        wdt:P625  ?sour .         # souřadnice
  OPTIONAL { ?obec wdt:P1082 ?obyvatel }
  FILTER (?obyvatel > 100000)
  SERVICE wikibase:label { bd:serviceParam wikibase:language "cs". }
}
ORDER BY DESC(?obyvatel)
```

<div class="small">

| obecLabel | ruian | obyvatel | sour |
|---|---|---|---|
| Praha | 554782 | 1397880 | Point(14.4214 50.0875) |
| Brno | 582786 | 402739 | Point(16.6083 49.1953) |
| Ostrava | 554821 | 283187 | Point(18.2925 49.8356) |

</div>

<div class="small">

**Kód RÚIAN** je spojovací klíč do ČSÚ, ČÚZK, volby.cz i Registru smluv; souřadnice zadarmo (na konci bude přednáška o prostorových datech :-)

</div>
</div>

Note:
Oficiální RDF endpoint RÚIANu (ruian.linked.opendata.cz) je dlouhodobě mimo
provoz -- ukázka toho, jak křehká ta infrastruktura umí být. Wikidata jsou
dnes spolehlivější cesta k témuž klíči.

---

# Propojit: prostorová data z OpenStreetMap

```sparql
PREFIX osmkey: <https://www.openstreetmap.org/wiki/Key:>
PREFIX geo:    <http://www.opengis.net/ont/geosparql#>

SELECT ?jmeno ?wikidata ?wkt WHERE {
  ?osm osmkey:amenity  "university" ;
       osmkey:name     ?jmeno ;
       osmkey:wikidata ?wikidata ;
       geo:hasGeometry/geo:asWKT ?wkt .
  FILTER(CONTAINS(?jmeno, "Brn"))
}
```

- Endpoint [qlever.dev](https://qlever.dev/osm-planet) -- celý OpenStreetMap jako RDF
- Geometrie přijde ve formátu **WKT**, který načte PostGIS
- VUT nemá jednu budovu, zkusme ``Fakulta inform''

Note:
Mendelova univerzita → Q1783765, Veterinární univerzita → Q7896530.
Všimněte si property path `geo:hasGeometry/geo:asWKT` -- dva skoky jedním
výrazem.

---

# Ověřit: federace přes dva endpointy

<div class="small">

Wikidata se **9. 5. 2025 rozdělila na dva grafy** -- vědecké články byly přes polovinu trojic a přestalo se to vejít na jeden stroj.

```sparql
PREFIX wdsubgraph: <https://query.wikidata.org/subgraph/>

SELECT ?jmeno ?nar WHERE {
  VALUES ?clanek { wd:Q29164671 }
  ?clanek wdt:P50 ?autor .                    # článek → autoři
  SERVICE wdsubgraph:wikidata_main {          # skok do druhého grafu
    ?autor wdt:P569 ?nar ; rdfs:label ?jmeno .
    FILTER(LANG(?jmeno) = "cs")
  }
}
```

```
Tim Berners-Lee 1955-06-08 | James Hendler 1957-04-02
```

<p class="xfragment" style="text-align: center; font-size: 125%;"><code>Q29164671</code> je článek <em>The Semantic Web</em> z roku 2001 &ndash; <br>ta citace, kterou dnešní přednáška začala.</p>

</div>

Note:
Spouštět na query-scholarly.wikidata.org. Dva gotche, které stojí za zmínku:
SERVICE wikibase:label tu nefunguje (popisky žijí v hlavním grafu, takže se
rdfs:label musí tahat uvnitř bloku SERVICE), a federovaný dotaz je pomalý
a spadne, když druhý endpoint neodpoví.

Partitioning z 7. přednášky dorazil o pět přednášek dřív -- a SERVICE je
distribuované zpracování dotazu.

---

# Česká otevřená data

Na úvodní přednášce jsem tvrdil, že se u nás publikuje nejvíc v XML.

<div class="col small">

```sparql
PREFIX dcat:<http://www.w3.org/ns/dcat#>
PREFIX dct:<http://purl.org/dc/terms/>

SELECT ?format
       (COUNT(DISTINCT ?d) AS ?n)
WHERE {
  ?d    a dcat:Dataset ;
        dcat:distribution ?dist .
  ?dist dct:format ?format .
}
GROUP BY ?format
ORDER BY DESC(?n)
```

</div>
<div class="col small">

| formát | sad | | formát | sad |
|---|---|---|---|---|
| ZIP | 11 890 | | JSON-LD | 1 130 |
| **XML** | **11 782** | | GeoJSON | 796 |
| CSV | 5 126 | | KML | 714 |
| JSON | 1 823 | | HTML | 581 |

</div>

@@div style="clear:both"@@@@/div@@

Endpoint [data.gov.cz/sparql](https://data.gov.cz/sparql)

---

# Katalog jako graf: vstup do projektu

<div class="small">

URL ke stažení všech CSV o kvalitě ovzduší

```sparql
PREFIX dcat:<http://www.w3.org/ns/dcat#>
PREFIX dct:  <http://purl.org/dc/terms/>

SELECT DISTINCT ?nazev ?url WHERE {
  ?ds   a dcat:Dataset ; dct:title ?nazev ; dcat:distribution ?dist .
  ?dist dcat:downloadURL ?url ; dct:format ?f .
  FILTER(STRENDS(STR(?f), "file-type/CSV"))
  FILTER(CONTAINS(LCASE(?nazev), "ovzduší"))
}
```

```
Kvalita ovzduší – aktuální hodinové údaje   opendata.chmi.cz/air_quality/
Kvalita ovzduší – data z mobilních stanic   data.brno.cz/api/download/…
Emise znečišťujících látek (REZZO 1–4)      data.csu.gov.cz/opendata/…
```

- Výstupem dotazu je **seznam URL** -- ten rovnou pustíte do `curl` z minulé přednášky
- Metadata katalogu jsou graf; dotazuji se tedy **na data o datech**

</div>

---

# Transformace pomocí CONSTRUCT

```sparql
PREFIX ex: <https://upa.fit.vut.cz/def#>

CONSTRUCT {
  ?obec ex:ruianKod ?ruian ; ex:nazev ?jmeno ;
        ex:pocetObyvatel ?obyvatel .
} WHERE {
  ?obec wdt:P31 wd:Q5153359 ; wdt:P7606 ?ruian ;
        wdt:P1082 ?obyvatel ; rdfs:label ?jmeno .
  FILTER(LANG(?jmeno) = "cs" && ?obyvatel > 20000)
}
```

- Výsledkem **není tabulka, ale graf** -- přemapovaný na můj vlastní slovník
- Tento výstup nahraju do svého úložiště a dál se ptám jen na něj
- **ETL transformace**, zapsaná deklarativně

---

# Kde to naráží

- **Timeouty a rate limity** -- veřejný endpoint vám velký dotaz nedopočítá
- **Nerovnoměrné pokrytí** -- Wikidata vědí o Brně všechno a o malé firmě nic
- **Kvalita** -- historické hodnoty, chybějící kvalifikátory, volně použité `owl:sameAs`
- **Dostupnost** -- endpoint je cizí server; dnes běží, zítra vrací 502 (viz RÚIAN)
- Vždy lze dump **stáhnout a nahrát do lokálního úložiště**
  - Fuseki, Oxigraph, QLever (Ukládání a Příprava Dat :-)
  - Umožňuje propojit datasety v jednom úložišti (viz podgrafy)
