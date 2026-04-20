# Multimedia `<audio>`

  - The `controls` attribute displays the controls (play, stop, pause)
  - JavaScript API for controlling the playback

```html
<audio controls>
   <source src="sound.ogg" type="audio/ogg">
   <source src="sound.mp3" type="audio/mpeg">
   Audio is not supported.
</audio>
``` 

<audio controls>
   <source src="https://www.fit.vut.cz/study/course/ITW/public/assets/sample-5.ogg" type="audio/ogg">
   Audio is not supported.
</audio>


  - Different supported formats and codecs (MP3, WAW, OGG, ...)
  - Browser-dependent 

---

# Multimedia `<video>`

```html
<video controls height="240" width="320">
   <source src="file.mp4" type="video/mp4">
   <source src="file.ogg" type="video/ogg">
   Video is not supported.
 </video>
``` 

<video controls height="480" width="640" style="position: absolute; right: 5em; bottom: 3em;">
   <source src="https://www.fit.vut.cz/study/course/ITW/public/assets/sample-5.mp4" type="video/mp4">
   Video is not supported.
 </video>

  - Different supported formats and codecs (MP4, WebM, OGG, ...)
  - Browser-dependent 

---

# Vector Graphics `<svg>`

  - SVG a MathML may be included directly in the document
    - with `xmlns` *namespace definition* optional in HTML
    - note the XML syntax discussed later

<pre class="code-render" default-style="" resizable="false" style="width: 400px; height: 270px; float: right; z-index: 1; margin: 2rem">
 <svg height="120"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="50" fill="red" />
  <rect x="80" y="20" height="60" width="60"
        style="stroke:none; fill:#00ff00;
        fill-opacity: 0.5;" />
</svg> 
</pre>

```xml
<svg height="120" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="50" fill="red" />
  <rect x="80" y="20" height="60" width="60"
        style="stroke:none; fill:#00ff00;
        fill-opacity: 0.5;" />
</svg> 
```

  - Or use the SVG files as any other image

```html
<img width="200" height="120" src="figure.svg">
```

<span class="note">See details on <a href="https://developer.mozilla.org/en-US/docs/Web/SVG">MDN</a></span>

---

# Inline frame

<iframe width="800" height="400" src="assets/examples/iframedoc.html" sandbox="allow-scripts allow-same-origin allow-popups allow-forms">
Inline frames are not supported.
</iframe>

<div class="">

```html
<iframe width="400" height="400" src="iframedoc.html">
Inline frames are not supported.
</iframe>
```

- Document is displayed in a separate context; it should not be able to access or influence the parent document.

</div>

---

# ARIA

  - **Accessible Rich Internet Applications** — W3C standard
  - Adds accessibility semantics for assistive technologies (screen readers, etc.)
  - Does not change visual appearance — purely for programmatic exposure

  - **`role`** — declares the element's purpose
```html
<div role="navigation">...</div>
<div role="dialog" aria-modal="true">...</div>
```
  - **`aria-*` state and property attributes**
```html
<button aria-expanded="false" aria-controls="menu">Menu</button>
<input aria-required="true" aria-describedby="hint">
<span id="hint">Must be a valid email</span>
```

<span class="note"><a href="https://www.w3.org/TR/wai-aria/">WAI-ARIA specification</a>,</span>
<span class="note"><a href="https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA">MDN ARIA</a></span>

---

# ARIA: Landmark Roles

  - Landmarks divide the page into navigable regions — screen readers let users jump between them

| Role | Equivalent element | Purpose |
|---|---|---|
| `banner` | `<header>` | Site-wide header |
| `navigation` | `<nav>` | Navigation links |
| `main` | `<main>` | Primary content |
| `complementary` | `<aside>` | Supporting content |
| `contentinfo` | `<footer>` | Site-wide footer |
| `search` | `<search>` | Search widget |
| `form` | `<form>` | Form region |

  - Prefer **semantic HTML elements** — they carry the role implicitly; use `role` only when semantics can't be expressed otherwise

<span class="note"><a href="https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles">ARIA Roles on MDN</a></span>

---

# Structured Data & the Semantic Web

  - Goal: embed **machine-readable semantics** into HTML pages
  - Based on **RDF** (Resource Description Framework) — W3C standard
    - Data model: *subject – predicate – object* triples
    - Resources identified by URIs
  - **[Schema.org](https://schema.org)** — shared vocabulary of types and properties
    - Maintained by Google, Microsoft, Apple, Yandex
    - Covers: people, organizations, products, events, reviews, ...
    - Used as the standard `itemtype` / `@type` vocabulary

<span class="note"><a href="https://www.w3.org/RDF/">W3C RDF</a>,</span>
<span class="note"><a href="https://schema.org">Schema.org</a></span>

---

# Microdata

  - Add semantics to HTML elements using specific attributes
  - Attributes: 
    - **itemscope** – item set container
    - **itemprop** – a property
    - **itemtype** – element type denoted as URL
    - **itemid** – a global identifier (e.g. ISBN for books)
    - **itemref** – global identifier reference

  - Example using [Schema.org](https://schema.org) vocabulary
  
```html
<div itemscope="" itemtype="https://schema.org/Person">
 <p>My name is <span itemprop="givenName">John</span>.</p>
 <p>My surname is <span itemprop="familyName">Smith</span>.</p>
 <p>I was born in <span itemprop="birthPlace">Brno</span>.</p>
</div>
```

---

# JSON-LD

  - **JSON for Linking Data** — W3C recommendation, preferred by Google
  - Embedded in a `<script>` tag — **no need to annotate HTML markup**
  - Cleaner separation of data and presentation

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Person",
  "givenName": "John",
  "familyName": "Smith",
  "birthPlace": "Brno",
  "url": "https://example.org/john"
}
</script>
```

  - `@context` — declares the vocabulary (Schema.org)
  - `@type` — the type of the described entity
  - Other keys are Schema.org property names

<span class="note"><a href="https://json-ld.org/">JSON-LD</a>,</span>
<span class="note"><a href="https://schema.org">Schema.org</a></span>

---

# RDFa

  - **RDF in Attributes** — W3C recommendation, extends HTML with RDF attributes
  - More expressive than Microdata (full RDF support), but more complex syntax
  - Key attributes: `vocab`, `typeof`, `property`, `resource`, `prefix`

```html
<div vocab="https://schema.org/" typeof="Person">
  <p>My name is
    <span property="givenName">John</span>
    <span property="familyName">Smith</span>.
  </p>
  <p>I was born in
    <span property="birthPlace">Brno</span>.
  </p>
</div>
```

<span class="note"><a href="https://www.w3.org/TR/rdfa-primer/">W3C RDFa Primer</a></span>

---

# Structured Data Consumers

  - **[Google Search](https://developers.google.com/search/docs/appearance/structured-data/intro-structured-data)** — *rich results*: star ratings, FAQs, breadcrumbs, events, products, recipes
    - Supports JSON-LD (preferred), Microdata, RDFa
    - [Google Rich Results Test](https://search.google.com/test/rich-results)
  - **[Bing](https://www.bing.com/webmasters/help/marking-up-your-site-with-structured-data-3a93e731)** — similar rich results in search
  - **Social media** — related concept using `<meta>` tags:
    - *Open Graph* (Facebook, LinkedIn) — `og:title`, `og:image`, ...
    - *Twitter Cards* — `twitter:card`, `twitter:title`, ...
  - **Knowledge graphs** — Wikidata, DBpedia use linked data principles
