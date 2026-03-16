
<!-- .slide: class="section" -->

<header>
	<h1>RDF on the Web</h1>
	<p>Web of Documents vs. Web of Data</p>
</header>

---

# Semantic Annotations

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

- Links from HTML to semantic web concepts (URIs)
- Several standards exist
	- RDFa, HTML5 Microdata, JSON-LD
- Common crawl corpus
	- 2020: 50% (out of 3.4 billion) pages, 44.3% crawled domains
	- 2019: 37.9% (out of 2.45 billion) pages, 37.2% crawled domains

<p class="cite">Bizer, C.; Meusel, R.; Primpeli, A.: Web Data Commons - RDFa, Microdata, and Microformat Data Sets - <a href="http://webdatacommons.org/structureddata/index.html#toc4">Extraction Results from the September 2021 Common Crawl Corpus</a>.</p>

---

# The entire document annotation

```html
<html xmlns=“…”>
<head>
<rdf:RDF
    xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
    xmlns:dc="http://purl.org/dc/elements/1.1/">

  <rdf:Description rdf:about="http://www.about.me/"
    dc:creator="John Smith"
    dc:title="Document title"
    dc:description="A description"
    dc:date="2021-09-10"/>

</rdf:RDF>

</head>
```

---

# RDF and HTML integration
- HTML 5 – *Microdata* 
- W3C standard – *RDFa* 
- JSON notation – *JSON-LD*
- See e.g.
https://schema.org/Person#examples

---

# Another example – RDFa 

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

# Event RDFa example

An event (a conference)

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

The `event:whatever` attribute values are shortened URIs `http://www.w3.org/2002/12/cal#whatever` (not necessarily a functional link to the WWW, it is just an identifier).

---

# RDFa processing

1. RDFa parser
	- finding the elements and attributes in HTML
2. Representation of facts in the RDF way
	- Set of *subject -- predicate -- object* triples
3. Processing
	- Storage
		- RDF repository (*triple store*)
	- Serialization
		- Turtle, RDF/XML, JSON-LD, ...

https://www.w3.org/2012/pyRdfa

---

# Alternatively: JSON-LD

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

- Google is able to process structured data in HTML pages
- Both RDFa and JSON-LD
- Understands many schema.org vocabularies
- E.g. [Produts](https://developers.google.com/search/docs/data-types/product), [Movies](https://developers.google.com/search/docs/data-types/movie), [Recipes](https://developers.google.com/search/docs/data-types/recipe), ...
