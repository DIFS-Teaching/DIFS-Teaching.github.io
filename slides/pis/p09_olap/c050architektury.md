<!-- .slide: class="section" -->

<header>
	<h1>Architektury a konceptuální návrh</h1>
	<p>MOLAP, ROLAP, HOLAP, schémata</p>
</header>

---

# Architektury OLAP serveru

- **MOLAP** – Multidimensional OLAP
    - Vlastní multidimenzionální datové struktury (pole, řídké matice)
    - Rychlé indexování předzpracovaných agregovaných dat
    - Výhoda: maximální výkon; Nevýhoda: redundance, velké prostorové nároky
- **ROLAP** – Relational OLAP
    - Data uložena v **relačních tabulkách**, prezentována jako multidimenzionální pohled
    - Žádná redundance; Velká možnost škálování
- **HOLAP** – Hybrid OLAP
    - Kombinace obou přístupů – uživatelská flexibilita
- **Specializovaný SQL server**
    - Podpora SQL dotazů nad schématy hvězda/sněhová vločka

---

# Konceptuální modelování kostky – schémata

- **Schéma hvězdy** (_star schema_)
    - Jedna tabulka faktů ve středu, připojená k tabulkám dimenzí
- **Schéma sněhové vločky** (_snowflake schema_)
    - Zjemnění hvězdy: hierarchie dimenzí normalizovaná do více tabulek
- **Konstelace faktů** (_fact constellation / galaxy schema_)
    - Více tabulek faktů sdílejících tabulky dimenzí

---

# Fakta a dimenze

- **Tabulka faktů**
    - Největší tabulka v DB (zpravidla jediná)
    - Obsahuje **numerické míry** (tržba, počet, cena)
    - Cizí klíče do tabulek dimenzí
- **Tabulky dimenzí** (číselníky)
    - Logicky nebo hierarchicky uspořádané popisné údaje
    - Menší a mění se méně často
    - Nejčastěji: časová, geografická, produktová dimenze

---

# Schéma hvězdy (star schema)

- Každá relace dimenze sestává z atributů odpovídajících hodnotám dimenze
- **Neposkytuje explicitní podporu pro hierarchii** – lze obejít organizačně
- Relace dimenzí nejsou normalizované → jednoduché, ale pomalejší

```
          Branch
            │
    Time ───┼─── Sales Facts ───┬─── Item
            │    (time_key,      │
         Location  item_key,    Supplier
                  location_key,
                  branch_key,
                  euros_sold,
                  unit_sold)
```

---

# Schéma sněhové vločky (snowflake schema)

- Hierarchie dimenzí je **explicitně normalizována** do navázaných tabulek dimenzí
- Výhodná údržba relací dimenzí
- Příklad: dimenze Location → City (cizí klíč city_key) → Province → Country

```
Location ──→ City ──→ Province
Item     ──→ Supplier
Time     (flat, nebo rozložená)
```

- Složitější dotazy, ale lepší konzistence dat dimenzí

---

# Celkové schéma datového skladu

```
Produkční prostředí
  ├── Relační DB A  ┐
  ├── Relační DB B  ├── ETL ──→ Datový sklad ──→ OLAP ──→ Uživatelé
  └── Soubory, API ┘
```

**ETL**: Extraction → Transformation → Loading

- **Extrakce**: získání dat ze zdrojů
- **Transformace**: čištění, homogenizace, integrace
- **Načtení**: periodické doplňování datového skladu
