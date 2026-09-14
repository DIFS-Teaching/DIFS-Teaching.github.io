<!-- .slide: class="section" -->

<header>
    <h1>Ukládání dat</h1>
    <p>Kam data uložit a jak se na ně ptát. Přednášky 6 až 13.</p>
</header>

---

# Předpoklady, na kterých stojí relační model

<div style="font-size: 75%">

| Předpoklad z IDS | Kdy neplatí | Přednáška |
|---|---|---|
| Data jsou plochá a skalární | objekty, kolekce, dědičnost | Objektový přístup |
| Data se vejdou na jeden stroj | distribuce, výpadky | NoSQL I &ndash; CAP, BASE |
| Schéma znám dopředu a je pevné | heterogenní, měnící se data | NoSQL II, XML a JSON |
| Vztahy jsou vzácné, řeším je JOINem | vztah *je* ten hlavní obsah | grafové modely |
| Ptám se na rovnost nebo rozsah v 1D | &bdquo;blízko&ldquo;, &bdquo;uvnitř&ldquo;, podobnost | prostorové db, indexování |

</div>

- ??**Systematické představení návrhového prostoru**
- ??Jaké máme možnosti, když předpoklady s IDS neplatí?

Note:
Detail po přednáškách &ndash; zásoba komentářů k jednotlivým řádkům tabulky:

- **6. Objektový přístup.** Impedance mismatch, uživatelské typy, kolekce, dědičnost.
  Most z IDS do zbytku semestru &ndash; historicky první pokus rozšířit relační model
  *zevnitř*.
- **7. NoSQL I.** CAP a BASE, klíč-hodnota, partitioning. Klíčová myšlenka celé druhé
  poloviny: distribuce si kompromis vynutí. Nemáte na výběr, jestli platit &ndash; jen čím.
  A ten kompromis se propíše do datového modelu i do dotazovacího jazyka.
- **9. NoSQL II.** Sloupcové, dokumentové a grafové databáze, NewSQL. Návrh podle dotazů,
  ne podle dat &ndash; přesný opak normalizace z IDS. Denormalizace jako vědomé rozhodnutí,
  ne jako chyba.
- **10. Jazyky a systémy, případové studie.** Každý datový model má svůj jazyk, volba
  modelu je volba vyjadřovací síly dotazů. Syntetická přednáška, kde se obě poloviny
  předmětu potkají.
- **11. XML a JSON v databázích.** XPath a XQuery, JSONB, indexace cest. Zavírá dvě linky:
  scraping z první přednášky produkuje přesně tenhle druh dat, a je vidět, jak objektová
  rozšíření z šesté přednášky nakonec v praxi dopadla.
- **12. Prostorové databáze.** Geometrické typy, topologické operátory, R-stromy, PostGIS.
  Většina reálných dat má lokaci &ndash; objednávka, senzor, fotka, nehoda.
- **13. Indexování vícedimenzionálních dat.** Proč B-strom nad jednou dimenzí selže.
  R-stromy, k-d stromy, quad-tree, LSH. Vektorové databáze pro embeddingy jsou přesně
  tohle &ndash; základ dnešních RAG systémů.
