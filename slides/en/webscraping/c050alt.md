# Web APIs

- Some pages load the interesting content dynamically with JavaScript
	- `XMLHttpRequest` or `fetch()`
	- (formerly known as AJAX)
- The data source is an *HTTP endpoint*, that typically returns
	- HTML code snippets
	- or *Serialized structured data* -- JSON, XML, ...

E.g. https://www.uci.org/road/rankings again

---

# API Usage

- Slightly easier access to data <!-- .element: class="plus" -->
	- Usually one HTTP request is enough (GET or POST)
	- We parse a structured document
- The data format can be even more variable than a web page <!-- .element: class="minus" -->
	- Purely internal format of the application creators
- Efforts to complicate third party access <!-- .element: class="minus" -->
	- Authorization tokens, etc.
- There exist public endpoints with a well documented data format <!-- .element: class="plus" -->
	- E.g. [The official portal for European data](https://data.europa.eu/en)

---

# Web Page Annotations

- [Microformats](https://microformats.io/)
	- Annotation of HTML elements using predefined `class` values
	- A narrow set of defined formats
	- Easy implementation into an existing website
- Semantic technology, e.g. [RDFa](https://rdfa.info/)
	- HTML extension with new attributes (`resource`, `property`, ...)
	- Allows transformation of HTML to *linked data* represented by RDF
	- Identification of objects and properties using **URI**
	- There are a number of dictionaries (*ontologies*) for different domains
		- E.g. [FOAF](http://www.foaf-project.org/), [schema.org](https://schema.org/), ...
- See the [Semantic Web lecture](https://www.fit.vutbr.cz/~burgetr/val/2022/semantic_web_en)
