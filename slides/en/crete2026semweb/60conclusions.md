# Where It Hurts

- **Timeouts and rate limits** &ndash; a public endpoint won't finish your big query
    - Wikidata had to be **split in two graphs** in 2025 &ndash; scholarly articles had outgrown one server
- **Uneven coverage** &ndash; Wikidata knows everything about Knossos and nothing about the taverna next door
- **Quality** &ndash; historical values, sloppy `owl:sameAs`, marketing data in JSON-LD
- **Availability** &ndash; someone else's server: up today, `502` tomorrow
- Remedy: **download the dump**, load it into a local triple store (QLever, Oxigraph, Fuseki)

---

# Take-Aways

<div class="col3">

## 1. Things, not strings
Give things **global IRIs**, write facts as **triples**; graphs merge for free.

</div>
<div class="col3">

## 2. Reuse vocabularies
**schema.org**, Wikidata properties&hellip; define your own **only** when nothing fits.

</div>
<div class="col3">

## 3. SPARQL + LLM
Public graphs are one query away &ndash; and an AI with a SPARQL tool **writes those queries well**.

</div>

<div style="clear: both"></div>

<div class="callout">
Try it tonight: <a href="https://query.wikidata.org/">query.wikidata.org</a> &rarr; <em>Examples</em> &ndash; hundreds of ready-made queries to tweak.
</div>
