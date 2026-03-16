<!-- .slide: class="section" -->

<header>
	<h1>Alternativy</h1>
	<p>Je analýza HTML kódu jediná možnost?</p>
</header>

---

# Využití API

- Některé stránky načítají zajímavý obsah dynamicky JavaScriptem
	- `XMLHttpRequest` nebo `fetch()`
	- (aka AJAX)
- Zdrojem dat je *HTTP endpoint*, který typicky vrací
	- Útržky HTML kódu
	- *Serializovaná strukturovaná data* -- JSON, XML, ...

Opět např. https://www.uci.org/road/rankings

---

# Využití API

- Mírně jednodušší přístup k datům <!-- .element: class="plus" -->
	- Obvykle stačí jeden HTTP dotaz (GET nebo POST)
	- Parsujeme strukturovaný formát
- Formát dat může být ještě promněnlivější, než webová stránka <!-- .element: class="minus" -->
	- Čistě interní formát tvůrců aplikace
- Snaha komplikovat přístup třetích stran <!-- .element: class="minus" -->
	- Autorizační tokeny apod.
- Existují veřejné endpointy s dobře dokumentovaným formátem dat <!-- .element: class="plus" -->
	- Např. [Portál veřejně přístupných dat EU](https://data.europa.eu/euodp/cs/developerscorner)

---

# Anotace webových stránek

- [Microformats](https://microformats.io/)
	- Anotace HTML elementů pomocí předdefinovaných hodnot `class`
	- Úzká množina definovaných formátů
	- Snadná implementace do existujícího webu
- Sémantické technologie, např. [RDFa](https://rdfa.info/)
	- Rozšíření HTML o nové atributy (`resource`, `property`, ...)
	- Umožňuje transformaci HTML na *linked data* reprezentovaná pomocí RDF
	- Identifikace objektů a vlastností pomocí **URI**
	- Existuje celá řada slovníků (*ontologií*) pro různé domény
		- Např. [FOAF](http://www.foaf-project.org/), [schema.org](https://schema.org/), ...
- Viz přednáška [Sémanticky web](https://github.com/DIFS-Teaching/slides/tree/main/upa/semanticky_web)
