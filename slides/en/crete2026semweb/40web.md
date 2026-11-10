<!-- .slide: class="section" -->

<header>
    <p class="eyebrow">Part 03</p>
    <h1>Knowledge Graphs Hidden in Web Pages</h1>
    <p>Where search engines get their facts from</p>
</header>

---

# Look at the Page Source

A (made-up) taverna page in Heraklion contains this block, invisible to visitors:

<div class="col">

```html
<script type="application/ld+json">
{ "@context": "https://schema.org",
  "@type": "Restaurant",
  "name": "Taverna O Minotavros",
  "servesCuisine": "Cretan",
  "address": {
    "@type": "PostalAddress",
    "addressLocality": "Heraklion" },
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "4.7",
    "reviewCount": "312" }
}
</script>
```

</div>
<div class="col">

- **JSON-LD**: looks like plain JSON, **is** RDF
- `@context` maps short keys to IRIs: `"name"` &rArr; `https://schema.org/name`
- Vocabulary: **schema.org** (Google, Microsoft, Yahoo, Yandex)
- Older alternatives: Microdata, RDFa (attributes inside the HTML)

<div class="callout small">
~70 % of websites that annotate anything use JSON-LD; the average annotated page now carries <strong>~57 triples</strong>.
</div>

</div>

<div style="clear: both"></div>

<div class="cite">Web Data Commons, structured data extraction from Common Crawl 10/2024. <a href="https://webdatacommons.org/structureddata/">webdatacommons.org/structureddata</a></div>

Note:
Live: open any recipe or product page, view source, search for "ld+json". Paste it into
https://validator.schema.org/ to show the extracted graph.

---

# Why Would Anyone Bother?

- Search engines turn annotations into **rich results**: stars, prices, opening hours, recipes, events
- The website gets **more clicks** &ndash; a purely selfish reason, and that's why it works

<div class="col">

## Well covered
- Shops and products
- Recipes, events, local businesses
- News articles

</div>
<div class="col">

## The long tail
- Timetables, public records, small shops, university pages&hellip;
- **No annotations at all**
- And annotations may be **marketing**, not truth

</div>

<div style="clear: both"></div>

<div class="result">
For most of the web, the knowledge graph has to be <strong>extracted</strong> &ndash; nobody wrote it for us.
</div>

Note:
This is the bridge to the bonus part: if the page doesn't describe itself, we have to
describe it ourselves.
