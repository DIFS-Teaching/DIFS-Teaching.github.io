<!-- .slide: class="section" -->

<header>
    <p class="eyebrow">Part 02 &middot; Live</p>
    <h1>Asking the Graph: SPARQL</h1>
    <p>Pattern matching over billions of facts &ndash; everything on the following slides runs live</p>
</header>

---

# SPARQL: Draw the Pattern, Get the Matches

<span class="kicker">Which Greek islands have the most inhabitants?</span>

```sparql
SELECT ?island ?islandLabel ?population WHERE {
  ?island wdt:P31  wd:Q23442 ;      # ?island is an island
          wdt:P17  wd:Q41 ;         # ... in Greece
          wdt:P1082 ?population .   # ... with a population
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}
ORDER BY DESC(?population)
LIMIT 10
```

- The query is a **graph with holes** (`?variables`); the engine finds every way to fill them
- No tables, no JOIN: a join is just **the same variable used twice**
- [&#9654; Run on query.wikidata.org](https://query.wikidata.org/#SELECT%20%3Fisland%20%3FislandLabel%20%3Fpopulation%20WHERE%20%7B%0A%20%20%3Fisland%20wdt%3AP31%20%20wd%3AQ23442%20%3B%20%20%20%20%20%20%23%20%3Fisland%20is%20an%20island%0A%20%20%20%20%20%20%20%20%20%20wdt%3AP17%20%20wd%3AQ41%20%3B%20%20%20%20%20%20%20%20%20%23%20...%20in%20Greece%0A%20%20%20%20%20%20%20%20%20%20wdt%3AP1082%20%3Fpopulation%20.%20%20%20%23%20...%20with%20a%20population%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7D%0AORDER%20BY%20DESC%28%3Fpopulation%29%0ALIMIT%2010)

Note:
Ask the room to guess the top 3 before running. Crete wins easily (623k), then Euboea.
Students with SQL background: the three triple patterns are like three self-joins
on one big (subject, predicate, object) table.

---

# Wait &ndash; Why Is Rhodes There Twice?

<div class="col small">

| islandLabel | population |
|---|---|
| Crete | 623 065 |
| Euboea | 191 206 |
| **Rhodes** | **127 613** |
| **Rhodes** | **115 490** |
| **Corfu** | **100 854** |
| **Corfu** | **99 134** |
| Lesbos | 83 800 |

</div>
<div class="col">

- Wikidata stores the population **for 2011 and for 2020** &ndash; both are true!
- Multi-valued property &rArr; every combination becomes a row
- Your &ldquo;top 10&rdquo; silently became a top 8

<div class="callout small">

Fixes: aggregate (`MAX`, `GROUP BY`), filter by the date qualifier, or ask only for the *preferred* value.

</div>

</div>

<div style="clear: both"></div>

<div class="result">
A knowledge graph stores <strong>facts with history</strong>, not a single &ldquo;current row&rdquo;.
</div>

Note:
Let them guess why before revealing the right column. This is the most common
surprise for people coming from relational databases.

---

# Results Don't Have to Be Tables

<span class="kicker">All archaeological sites in the Crete Region &ndash; on a map</span>

```sparql
#defaultView:Map
SELECT DISTINCT ?site ?siteLabel ?coords ?image WHERE {
  ?site wdt:P31/wdt:P279* wd:Q839954 ;   # an archaeological site (or any subtype)
        wdt:P131+ wd:Q1267522 ;          # somewhere inside the Crete Region
        wdt:P625 ?coords .               # with coordinates
  OPTIONAL { ?site wdt:P18 ?image }
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}
```

- `/`, `*`, `+` are **property paths**: &ldquo;type or a subtype of it&rdquo;, &ldquo;located in, transitively&rdquo;
- **~250 sites** &ndash; click a dot to see the photo
- [&#9654; Run on query.wikidata.org](https://query.wikidata.org/#%23defaultView%3AMap%0ASELECT%20DISTINCT%20%3Fsite%20%3FsiteLabel%20%3Fcoords%20%3Fimage%20WHERE%20%7B%0A%20%20%3Fsite%20wdt%3AP31%2Fwdt%3AP279%2A%20wd%3AQ839954%20%3B%20%20%20%23%20an%20archaeological%20site%20%28or%20a%20subtype%29%0A%20%20%20%20%20%20%20%20wdt%3AP131%2B%20wd%3AQ1267522%20%3B%20%20%20%20%20%20%20%20%20%20%23%20somewhere%20in%20the%20Crete%20Region%0A%20%20%20%20%20%20%20%20wdt%3AP625%20%3Fcoords%20.%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20with%20coordinates%0A%20%20OPTIONAL%20%7B%20%3Fsite%20wdt%3AP18%20%3Fimage%20%7D%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7D)

Note:
Knossos sits in "Heraklion Municipality", which is in "Heraklion Regional Unit", which is
in "Crete Region" -- the `+` walks that chain. Without DISTINCT you get duplicates, because
there are several paths through the class hierarchy. Some sites (e.g. Lissos) have two
coordinates -- the same multi-value lesson again.

---

# &hellip; or a Photo Album

<span class="kicker">Monasteries of Crete</span>

```sparql
#defaultView:ImageGrid
SELECT DISTINCT ?m ?mLabel ?image WHERE {
  ?m wdt:P31 wd:Q44613 ;          # a monastery
     wdt:P131+ wd:Q1267522 ;      # in the Crete Region
     wdt:P18 ?image .             # that has a photo
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}
```

- Only change: one comment line selects the view
- [&#9654; Run on query.wikidata.org](https://query.wikidata.org/#%23defaultView%3AImageGrid%0ASELECT%20DISTINCT%20%3Fm%20%3FmLabel%20%3Fimage%20WHERE%20%7B%0A%20%20%3Fm%20wdt%3AP31%20wd%3AQ44613%20%3B%20%20%20%20%20%20%20%20%20%20%23%20a%20monastery%0A%20%20%20%20%20wdt%3AP131%2B%20wd%3AQ1267522%20%3B%20%20%20%20%20%20%23%20in%20the%20Crete%20Region%0A%20%20%20%20%20wdt%3AP18%20%3Fimage%20.%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20that%20has%20a%20photo%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7D)

Note:
Ask whether anyone has visited Toplou or Arkadi. Optional slide -- skip if running late.

---

# One City, Eighty Names

<span class="kicker">DBpedia: &ldquo;which other IRIs mean the same Heraklion?&rdquo;</span>

```sparql
SELECT ?same WHERE { dbr:Heraklion owl:sameAs ?same }
```

<div class="col">

```
wd:Q160544                  ← Wikidata
sws.geonames.org/261745     ← GeoNames
viaf.org/viaf/162900004     ← library catalogues
musicbrainz.org/area/4f3c…  ← music database
it.dbpedia.org/Candia       ← Italian Wikipedia
tr.dbpedia.org/Kandiye      ← Turkish Wikipedia
el.dbpedia.org/Ηράκλειο_Κρήτης
… 80+ links
```

</div>
<div class="col">

- `owl:sameAs` = &ldquo;these two IRIs denote **the same thing**&rdquo;
- Entity matching that **somebody already did and published**
- Spot the history: *Candia* (Venetian), *Kandiye* (Ottoman)
- But beware: the `sameAs` claim can't be always trusted

[&#9654; Run on dbpedia.org/sparql](https://dbpedia.org/sparql?default-graph-uri=http%3A%2F%2Fdbpedia.org&query=SELECT%20%3Fsame%20WHERE%20%7B%20dbr%3AHeraklion%20owl%3AsameAs%20%3Fsame%20%7D&format=text%2Fhtml)

</div>

<div style="clear: both"></div>

Note:
The two GND IDs are 4027652-1 and 2065535-6; typically one is the city, the other a
historical or administrative entity. owl:sameAs formally means "identical in every
respect", so importing it blindly merges things that should stay apart.

---

# OpenStreetMap as a Graph

```sparql
PREFIX osmkey: <https://www.openstreetmap.org/wiki/Key:>
PREFIX osmrel: <https://www.openstreetmap.org/relation/>
PREFIX ogc:    <http://www.opengis.net/rdf#>

SELECT ?amenity (COUNT(?x) AS ?count) WHERE {
  osmrel:453129 ogc:sfContains ?x .     # everything inside the island of Crete
  ?x osmkey:amenity ?amenity .
  FILTER(?amenity IN ("restaurant", "cafe", "bar", "place_of_worship"))
}
GROUP BY ?amenity
ORDER BY DESC(?count)
```

<div class="col small">

| amenity | count |
|---|---|
| place_of_worship | **3 824** |
| restaurant | 2 496 |
| cafe | 976 |

</div>
<div class="col">

- Crete has **more churches than restaurants** (at least on the map)
- Plus **500 mapped beaches** &ndash; try `osmkey:natural "beach"`
  [&#9654;](https://qlever.dev/osm-planet/?query=PREFIX%20osmkey%3A%20%3Chttps%3A%2F%2Fwww.openstreetmap.org%2Fwiki%2FKey%3A%3E%0APREFIX%20osmrel%3A%20%3Chttps%3A%2F%2Fwww.openstreetmap.org%2Frelation%2F%3E%0APREFIX%20ogc%3A%20%20%20%20%3Chttp%3A%2F%2Fwww.opengis.net%2Frdf%23%3E%0A%0ASELECT%20%28COUNT%28%3Fx%29%20AS%20%3Fbeaches%29%20WHERE%20%7B%0A%20%20osmrel%3A453129%20ogc%3AsfContains%20%3Fx%20.%0A%20%20%3Fx%20osmkey%3Anatural%20%22beach%22%20.%0A%7D)
- [&#9654; Run on qlever.dev](https://qlever.dev/osm-planet/?query=PREFIX%20osmkey%3A%20%3Chttps%3A%2F%2Fwww.openstreetmap.org%2Fwiki%2FKey%3A%3E%0APREFIX%20osmrel%3A%20%3Chttps%3A%2F%2Fwww.openstreetmap.org%2Frelation%2F%3E%0APREFIX%20ogc%3A%20%20%20%20%3Chttp%3A%2F%2Fwww.opengis.net%2Frdf%23%3E%0A%0ASELECT%20%3Famenity%20%28COUNT%28%3Fx%29%20AS%20%3Fcount%29%20WHERE%20%7B%0A%20%20osmrel%3A453129%20ogc%3AsfContains%20%3Fx%20.%20%20%20%20%20%23%20everything%20inside%20Crete%0A%20%20%3Fx%20osmkey%3Aamenity%20%3Famenity%20.%0A%20%20FILTER%28%3Famenity%20IN%20%28%22restaurant%22%2C%20%22cafe%22%2C%20%22bar%22%2C%20%22place_of_worship%22%29%29%0A%7D%0AGROUP%20BY%20%3Famenity%0AORDER%20BY%20DESC%28%3Fcount%29)

</div>

<div style="clear: both"></div>

Note:
Relation 453129 is the island of Crete in OSM (its osmkey:wikidata is Q34374, so it
links back to Wikidata). Ask the room to guess the ranking before showing the table.
Numbers as of November 2026. QLever (University of Freiburg) indexes the full planet,
tens of billions of triples, on one machine.
