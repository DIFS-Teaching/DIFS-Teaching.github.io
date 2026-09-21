<!-- .slide: class="section" -->

<header>
	<h1>RDF na Webu</h1>
	<p>Web of Documents vs. Web of Data</p>
</header>

---

# Sémantické anotace

<div class="col small">

- Propojení HTML a konceptů sémantického webu (IRI)
- Tři zápisy, jeden datový model:
	- **JSON-LD** -- blok JSONu v `<script>`, oddělený od obsahu
	- **Microdata** -- atributy `itemscope` / `itemprop`
	- **RDFa** -- atributy `vocab` / `typeof` / `property`
- Drtivě nejčastější slovník: **schema.org**

</div>
<div class="col small">

| Z webů, které něco anotují | podíl |
|---|---|
| JSON-LD | ≈ 70 % |
| Microdata | ≈ 46 % |
| RDFa | ≈ 3 % |

Průměrný počet trojic na stránku vzrostl z **10 (2015) na 57 (2024)**.

</div>

@@div style="clear:both"@@@@/div@@

<p class="cite" style="font-size: 75%">Web Data Commons: Microdata, RDFa, JSON-LD and Microformat Data Sets, vydání leden 2025 (extrakce z korpusu Common Crawl 10/2024). <a href="https://webdatacommons.org/structureddata/">webdatacommons.org/structureddata</a></p>

Note:
Součet přes 100 % je správně -- řada webů používá dva formáty naráz, typicky
Microdata ze starší šablony a JSON-LD z novějšího pluginu.

---

# JSON-LD: nejrozšířenější zápis

<div class="small">

```html
<script type="application/ld+json">
{ "@context": "https://schema.org",
  "@type": "Product",
  "name": "Kávovar Aurora 2",
  "offers": {
    "@type": "Offer",
    "price": "4990",
    "priceCurrency": "CZK"
  }
}
</script>
```

- `@context`: mapuje krátké klíče na IRI
	- `"name"` ⇒ `https://schema.org/name`
- Běžná aplikace vidí obyčejný JSON, RDF nástroj jako graf
- JSON-LD 1.1 je **W3C Recommendation** (2020)

</div>

---

# Microdata a RDFa

<div class="col small">

**Microdata** -- v HTML5

```html
<div itemscope
  itemtype="https://schema.org/Person">
  <span itemprop="name">Jan Novák</span>
</div>
```

</div>
<div class="col small">

**RDFa 1.1 Lite** -- W3C standard

```html
<div vocab="https://schema.org/"
  typeof="Person">
  <span property="name">Jan Novák</span>
</div>
```

</div>

@@div style="clear:both"@@@@/div@@


- Obojí anotuje **přímo zobrazovaný obsah** -- nehrozí rozpor mezi tím, co vidí člověk a co stroj
- Zato se to rozbije při každé změně šablony -- proto JSON-LD vyhrál
- Zkrácený zápis (`schema:Person`) se expanduje na plné IRI podle `vocab` / `prefix`

---

# Zpracování anotací

<div class="small">

1. **Parser** -- najde anotace v HTML (všechny tři zápisy naráz)
2. **Model** -- převede je na množinu trojic
3. **Zpracování** -- uloží do triplestoru, nebo serializuje (Turtle, JSON-LD, ...)

```python
import requests, extruct

html = requests.get(url).text
data = extruct.extract(html, base_url=url,
                       syntaxes=["json-ld", "microdata", "rdfa"])
```

- Ověřovací nástroje: [Schema Markup Validator](https://validator.schema.org/) · [Google Rich Results Test](https://search.google.com/test/rich-results)
- V Pythonu dál [`rdflib`](https://rdflib.readthedocs.io/) -- trojice, SPARQL nad nimi, serializace

<p class="fragment" style="text-align: center; font-size: 130%;"><strong>Z HTML na trojice ve třech řádcích &ndash; místo tří set řádků scraperu.</strong></p>

</div>

Note:
Tohle je přímé pokračování minulé přednášky: na konci té části o alternativách
ke scrapování jsme se dívali na JSON-LD v e-shopu a slíbil jsem, že vysvětlím,
co ta IRI znamenají. Teď to student má celé: IRI, slovník i nástroj.

---

# Proč to weby vůbec publikují

- Google a spol. z anotací staví **rich results** -- hvězdičky, ceny, recepty, události
- Publikující web za to dostane **lepší vzhled ve výsledcích vyhledávání**
- Dokumentace: [Produkty](https://developers.google.com/search/docs/appearance/structured-data/product), [Filmy](https://developers.google.com/search/docs/appearance/structured-data/movie), [Recepty](https://developers.google.com/search/docs/appearance/structured-data/recipe)

- Pokrytí je **nevyvážené** -- e-shopy, recepty, události a firmy ano; cokoli jiného spíš ne
- A publikovaná data jsou **marketingová** -- cena bez DPH, dostupnost ``skladem''

<p class="xfragment" style="font-size: 130%; text-align: center; margin-top: 0.6em;">Sémantický web a web jsou <strong>různé věci</strong>.</p>
<p class="fragment" style="font-size: 130%; text-align: center; margin-top: 0.6em;"><strong>RDF data mohou existovat bez WWW stránek.</strong></p>
Note:
Dobrá chvíle připomenout kritický odstup z minulé přednášky: že jsou data
strojově čitelná, neznamená, že jsou pravdivá. Jen se vám lépe stahují.

