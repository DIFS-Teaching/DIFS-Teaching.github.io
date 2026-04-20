<!-- .slide: class="section" -->

<header>
	<h1>Konceptuální návrh</h1>
	<p>Schémata datového skladu a architektury OLAP</p>
</header>

---

# Fakta a dimenze v relačním modelu

- Datová kostka se navrhuje v relačním modelu jako **tabulky**
- **Tabulka faktů**
	- největší tabulka v DB, zpravidla pouze jedna
	- obsahuje numerické měrné hodnoty (tržby, počty, náklady)
	- obsahuje cizí klíče do tabulek dimenzí
- **Tabulky dimenzí** (číselníky)
	- logicky nebo hierarchicky uspořádané údaje (textové popisky)
	- jsou menší a mění se méně často
	- typicky: časová, geografická, produktová dimenze

---

# Typické hierarchie dimenzí

```
Geografie:         Produkt:           Čas:
  Kontinent          Druh produktu      Rok
    └── Stát           └── Kategorie     └── Kvartál
          └── Kraj             └── Subkategorie  └── Měsíc
                └── Město               └── Název    └── Den
```

---

# Schéma hvězdy (Star Schema)

- **Jedna tabulka faktů** ve středu připojená k množině tabulek dimenzí
- Tabulky dimenzí nejsou normalizovány → **denormalizované**, ale snadno srozumitelné
- **Nevýhoda:** neposkytuje explicitní podporu pro hierarchii atributů

---

# Příklad – schéma hvězdy

<!-- .slide: class="normal centered" -->

```
          ┌──────────┐
          │  Čas     │
          │ time_key │
          │ day      │
          │ month    │
          │ year     │
          └────┬─────┘
               │
┌──────────┐   │   ┌──────────────────────────────┐
│  Odvětví │───┤   │  Fakta o prodeji              │
│branch_key│   ├───│  time_key  item_key           │
│branch_nm │   │   │  location_key  branch_key     │
└──────────┘   │   │  unit_sold  euros_sold        │
               │   └──────────────────────────────┘
┌──────────┐   │   ┌──────────┐
│  Položka │───┤   │ Umístění │
│ item_key │   └───│loc._key  │
│ item_name│       │ street   │
│ brand    │       │ city     │
└──────────┘       │ country  │
                   └──────────┘
```

---

# Schéma sněhové vločky (Snowflake Schema)

- Zjemnění hvězdičkového schématu: **hierarchie dimenzí** jsou normalizovány do navázaných tabulek
- Výhoda: **úspora místa**, snadnější údržba tabulek dimenzí
- Nevýhoda: denormalizovaná dimenze hvězdičkového schématu může být vhodnější pro rychlé procházení

---

# Příklad – sněhová vločka

```
  ┌──────────┐           ┌──────────┐
  │ Umístění │           │  Město   │
  │ loc._key │───────────│ city_key │
  │ street   │           │ city     │
  │ city_key │           │ province │
  └──────────┘           │ country  │
                         └──────────┘
```

_Dimenze Umístění je normalizována: tabulka Město je oddělena._

---

# Konstelace faktů (Galaxy Schema)

- **Více tabulek faktů**, které sdílejí tabulky dimenzí
- Lze chápat jako kolekci hvězd – proto také **schéma galaxie**
- Použití: různé obchodní procesy sdílející společné číselníky (čas, místo, produkt)

_Příklad: tabulka faktů o prodeji + tabulka faktů o dodávkách sdílí tabulky Čas, Produkt, Umístění_

---

# Architektury serveru OLAP

- **MOLAP** – Multidimensional OLAP
	- Data uložena ve vlastních multidimenzionálních strukturách (pole)
	- Rychlé indexování předzpracovaných agregátů
	- ✓ maximální výkon; ✗ redundance, velké prostorové nároky

- **ROLAP** – Relational OLAP
	- Data uložena v relačních tabulkách, multidimenzionální pohled vytváří prezentační vrstva
	- Velká škálovatelnost, žádná redundance
	- ✗ pomalejší přístup, omezené komplexní analýzy

- **HOLAP** – Hybrid OLAP
	- Kombinace: data v relačních tabulkách, agregace v multidimenzionálních strukturách
	- Využití multidimenzionální cache

---

# MOLAP vs. ROLAP – srovnání

| | MOLAP | ROLAP |
|---|---|---|
| Uložení dat | multidim. struktury | relační tabulky |
| Agregace | předpočítané | za běhu pomocí SQL |
| Výkon | vysoký | závisí na složitosti |
| Škálovatelnost | omezená | vysoká |
| Komplexní analýzy | bohatá knihovna funkcí | omezené |

<!-- ⚠️ ZASTARALÉ/ZBYTEČNÉ: Podrobné srovnání ROLAP vs. MOLAP v původním obsahu je příliš granulární (3 samostatné slidy). Stačí tato srovnávací tabulka. -->
