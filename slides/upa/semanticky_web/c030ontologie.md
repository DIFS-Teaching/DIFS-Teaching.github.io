<!-- .slide: class="section" -->

<header>
	<h1>Ontologie</h1>
	<p>Odkud se berou ty slovníky</p>
</header>

---

# Ontologie: k čemu to je

_„Formální, explicitní specifikace sdílené konceptualizace“_

<div class="col small">

**K čemu nám je**

- **Dodává význam jednotlivým IRI** -- bez ní je `wdt:P1082` jen řetězec
- **Umožňuje integraci dat z různých zdrojů** -- společný slovník místo párování názvů

</div>
<div class="col small">

**Z čeho se skládá**

- **Třídy** (`foaf:Person`), **individua** (`wd:Q14960`), **vlastnosti** (`foaf:knows`)
- *Objektové* vlastnosti míří na zdroj, *datatypové* na literál

</div>

@@div style="clear:both"@@@@/div@@

<p class="cite" style="font-size: 70%">Gruber, T. R.: A translation approach to portable ontology specifications. <em>Knowledge Acquisition</em> 5(2), 1993. Ve znění, které upřesnil Studer et al. (1998).</p>

Note:
Vrátit se sem k motivační části: tohle je ta druhá polovina odpovědi. Globální
identifikátor říká *která věc to je*, ontologie říká *co o ní tvrdím*.

---

# RDF Schema a OWL

<div class="small">

```turtle
@prefix rdf:   <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs:  <http://www.w3.org/2000/01/rdf-schema#> .
@prefix skola: <https://upa.fit.vut.cz/skola#> .

skola:Osoba    a rdfs:Class .
skola:Student  a rdfs:Class ;
               rdfs:subClassOf skola:Osoba .

skola:maZapsano  a rdf:Property ;
                 rdfs:domain skola:Student ;   # subjekt je Student
                 rdfs:range  skola:Predmet .   # objekt je Předmět
```

- **RDFS** -- třídy, hierarchie, `rdfs:domain` / `rdfs:range`, `rdfs:label`, `rdfs:comment`
- **OWL 2** (W3C Rec 2009, 2. vydání 2012) -- výrazně bohatší: ekvivalence, disjunktnost, kardinality, inverzní vlastnosti
</div>

Note:
`rdfs:domain` a `rdfs:range` nejsou kontrola! Neříkají &bdquo;sem smí jen Student&ldquo;,
ale &bdquo;co sem dáš, to je Student&ldquo;. Je to pravidlo pro odvozování, ne pro
validaci. Na to navazuje slajd o otevřeném světě.

---

# Propojování entit: owl:sameAs

<div class="small">

```turtle
dbr:Brno  owl:sameAs  wd:Q14960 ,
          <http://sws.geonames.org/3078610/> ,
          <http://viaf.org/viaf/144231825> .
```

- `owl:sameAs` -- **tytéž entity** popsané v různých datasetech
- `owl:differentFrom` -- explicitně různé; různá IRI sama o sobě nestačí
</div>

Note:
Tohle je nejpraktičtější konstrukt z celého OWL a zároveň nejvíc zneužívaný.
Za chvíli si ho vytáhneme z DBpedie a uvidíme, že mezi správnými odkazy je
i jeden špatný.

---

# Otevřený svět a SHACL

<div class="col small">

**Předpoklad otevřeného světa**

Chybějící tvrzení ≠ nepravda. &bdquo;O tomto produktu nevím cenu&ldquo; není
&bdquo;tento produkt nemá cenu&ldquo;.

V OWL proto **nejde** říct ``každý produkt musí mít cenu''.
`owl:minCardinality` *odvozuje*, že ta cena někde existuje --
nevaliduje, že je v datech.

</div>
<div class="col small">

**SHACL** (W3C Rec 2017)

Uzavřený svět, **schéma pro RDF**:

```turtle
ex:ProduktShape a sh:NodeShape ;
  sh:targetClass schema:Product ;
  sh:property [
    sh:path schema:price ;
    sh:minCount 1 ;
    sh:datatype xsd:decimal ] .
```

Výstupem je *validation report*: co v datech chybí.

</div>

---

# Reálně používané slovníky (ontologie)

<div style="font-size: 88%">

<div class="col small">

- **[schema.org](https://schema.org/)** -- de facto slovník webu
	- Google, Microsoft, Yahoo, Yandex
	- `Product`, `Offer`, `Organization`, `Event`
	- Uvidíme za chvíli v JSON-LD
- **[DCAT / DCAT-AP-CZ](https://ofn.gov.cz/dcat-ap-cz-rozhran%C3%AD-katalog%C5%AF-otev%C5%99en%C3%BDch-dat/)** -- katalogy datových sad
	- Slovník za `data.gov.cz`, použitelný v projektu
- **[SKOS](https://www.w3.org/TR/skos-reference/)** -- taxonomie, číselníky, tezaury

</div>
<div class="col small">

- **[PROV-O](https://www.w3.org/TR/prov-o/)** -- provenience
	- Odkud data jsou, kdo je vytvořil, čím
- **[GeoSPARQL](https://www.ogc.org/standards/geosparql)** -- geometrie a prostorové dotazy (přednáška 12)
- **[Dublin Core (DCMI Terms)](https://www.dublincore.org/specifications/dublin-core/dcmi-terms/)** -- metadata dokumentů
- **[OWL-Time](https://www.w3.org/TR/owl-time/)** -- časové intervaly

</div>

@@div style="clear:both"@@@@/div@@


<div class="small">

- Rejstřík slovníků: **[Linked Open Vocabularies](https://lov.linkeddata.es/dataset/lov/)** &middot; editor: [Protégé](https://protege.stanford.edu/) &middot; historické, ale pořád v datech: **FOAF**

</div>

<p style="text-align: center; font-size: 115%; margin-top: 0.2em;">Vlastní ontologii tvořte až <strong>když není vyhnutí</strong>. Napřed hledejte existující.</p>

</div>
