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

Opět např. [žebříček UCI](https://www.uci.org/discipline/road/6TBjsDD8902tud440iv1Cu?tab=rankings&discipline=ROA) &ndash; podívejte se do záložky **Network**

---

# Využití API: Pros & Cons

- Mírně jednodušší přístup k datům <!-- .element: class="plus" -->
	- Obvykle stačí jeden HTTP dotaz (GET nebo POST)
	- Parsujeme strukturovaný formát
- Formát dat může být ještě proměnlivější, než webová stránka <!-- .element: class="minus" -->
	- Čistě interní formát tvůrců aplikace
- Snaha komplikovat přístup třetích stran <!-- .element: class="minus" -->
	- Autorizační tokeny apod.
- Existují veřejné endpointy s dobře dokumentovaným formátem dat <!-- .element: class="plus" -->
	- Např. [Portál otevřených dat EU](https://data.europa.eu/) nebo [NKOD](https://data.gov.cz/)

---

# Anotace webových stránek

Data pro stroje **přímo ve stránce**, vedle dat pro člověka.

- **JSON-LD** &ndash; dnes nejrozšířenější, samostatný blok v `<head>`

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Quip Kids Electric Toothbrush",
  "offers": { "@type": "Offer", "price": "25.00", "priceCurrency": "USD" }
}
</script>
```

- **Microdata** a [**RDFa**](https://rdfa.info/) &ndash; anotace rozptýlená v atributech existujících elementů
- [Microformats](https://microformats.io/) &ndash; historicky první pokus, anotace hodnotami `class`

---

# Proč je to pro nás dobrá zpráva

- Údaje jsou **explicitně pojmenované** &ndash; žádné hádání podle pozice v tabulce
- Identifikace objektů a vlastností pomocí **URI**
	- Celá řada slovníků (*ontologií*) pro různé domény, např. [schema.org](https://schema.org/)
- Umožňuje transformaci HTML na *linked data* reprezentovaná pomocí RDF
- ??Kdo to publikuje? Každý, kdo chce vypadat dobře ve výsledcích vyhledávání
- ??Jsme na **horním konci žebříku** z úvodu přednášky

<p class="fragment">
Co ty URI znamenají, odkud se berou slovníky a jak se v takových datech dotazuje
&ndash; <a href="https://gitshow.net/https/difs-teaching.github.io/slides/upa/semanticky_web">příští přednáška</a>.
</p>
