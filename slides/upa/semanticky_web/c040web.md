
<!-- .slide: class="section" -->

<header>
	<h1>RDF na Webu</h1>
	<p>Web of Documents vs. Web of Data</p>
</header>

---

# Sémantické Anotace

@@div class="xfragment" style="float:right; font-size: 50%; top: 0; right: 0; width: 35em; max-height: 50%;"@@
```html
<div itemscope itemtype="https://schema.org/Person">
    <span itemprop="name">Jane Doe</span>
    <span itemprop="jobTitle">Professor</span>
    <div itemprop="address" itemscope itemtype="https://schema.org/PostalAddress">
        <span itemprop="streetAddress">
          20341 Whitworth Institute
          405 N. Whitworth
        </span>
        <span itemprop="addressLocality">Seattle</span>,
        <span itemprop="addressRegion">WA</span>
        <span itemprop="postalCode">98052</span>
    </div>
</div>
```
@@/div@@

- Propojení HTML a konceptů sémantického webu (URI)
- Několik existujících standardů
	- RDFa, HTML5 Microdata, JSON-LD
- Common crawl corpus
	- 2020: 50% (z 3.4 miliard) stránek, 44.3% zpracovaných domén
	- 2019: 37.9% (z 2.45 miliard) stránek, 37.2% zpracovaných domén

<p class="cite">Bizer, C.; Meusel, R.; Primpeli, A.: Web Data Commons - RDFa, Microdata, and Microformat Data Sets - <a href="http://webdatacommons.org/structureddata/index.html#toc4">Extraction Results from the September 2021 Common Crawl Corpus</a>.</p>

---

# Integrace RDF a HTML
- HTML 5 – *Microdata* 
- W3C standard – *RDFa* 
- JSON notace – *JSON-LD*
- Viz např.
https://schema.org/Person#examples

---

# Jiný příklad – RDFa 

```html
<p xmlns:dc="http://purl.org/dc/elements/1.1/"
   about="http://www.example.com/books/wikinomics">

  In his latest book
  <cite property="dc:title">Wikinomics</cite>,
  <span property="dc:creator">Don Tapscott</span>
  explains deep changes in technology,
  demographics and business.
  The book is due to be published in
  <span property="dc:date" content="2006-10-01">October 2006</span>.

</p>
```

---

# Událost v RDFa

Popis události (konference)

```html
<div xmlns:event="http://www.w3.org/2002/12/cal#" typeof="event:Vevent">
     <h3 property="event:summary">WWW 2009</h3>
     <p property="event:description">18th International World Wide Web Conference</p>
     <p>To be held from
        <span property="event:dtstart" content="2009-04-20">20th April 2009</span>
        until <span property="event:dtend" content="2009-04-24">24th April</span>,
        in <span property="event:location">Madrid, Spain</span>.</p>
</div>
```

Hodnoty atributů `event:cokoliv` jsou zkráceným zápisem URI `http://www.w3.org/2002/12/cal#cokoliv` (nemusí jít nutně o funkční odkaz na WWW, je to jen identifikátor).

---

# Zpracování RDFa

1. RDFa parser
	- nalezení elementů a atributů v HTML
2. Reprezentace obecným modelem RDF
	- Množina trojic *subjekt -- predikát -- objekt*
3. Zpracování
	- Uložení
		- Úložiště RDF (*triple store*)
	- Serializace
		- Turtle, RDF/XML, JSON-LD, ...


https://www.w3.org/2012/pyRdfa

---

# Alternativa: JSON-LD

```html
<html>
  <head>
    <title>WWW 2009</title>
    <script type="application/ld+json">
    {
        "@context": ""http://www.w3.org/2002/12/cal#",
        "@type": [ "Vevent" ],
        "description": "18th International World Wide Web Conference",
        "dtend": "2009-04-24",
        "dtstart": "2009-04-20",
        "location": "Madrid, Spain",
        "summary": "WWW 2009"
	}    
    </script>
  </head>
  <body>
  <h2>WWW 2009</h2>
  <p>
	The 18th International World Wide Web Conference took
	part in 2009 in Madrid, Spain.
  </p>
  </body>
</html>
```

https://json-ld.org/

---

# Google Structured Data

- Google zpracovává strukturovaná data v HTML stránkách
- RDFa i JSON-LD
- Podporuje mnoho slovníků schema.org
- Např. [Produkty](https://developers.google.com/search/docs/data-types/product), [Filmy](https://developers.google.com/search/docs/data-types/movie), [Recepty](https://developers.google.com/search/docs/data-types/recipe), ...

