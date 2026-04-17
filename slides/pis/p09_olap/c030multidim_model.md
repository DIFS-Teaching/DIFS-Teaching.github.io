<!-- .slide: class="section" -->

<header>
	<h1>Multidimenzionální model</h1>
	<p>Dimenze, fakta, kostka</p>
</header>

---

# Dimenze

- **Dimenze** je _uspořádatelná_ množina hodnot _diskrétního_ základního typu
  (integer, výčet, čas) nebo množina jejich struktur **hierarchicky organizovaných**
- Příklady dimenzí:
    - **Čas**: leden, únor, …, prosinec (nebo rok → kvartál → měsíc → den)
    - **Místo**: Praha, Brno, Ostrava, Plzeň, … (nebo kontinent → země → město)
    - **Produkt**: kabáty, kalhoty, bundy, čepice, trička, …

---

# Hierarchická dimenze

- Jednorozměrná dimenze: flat seznam hodnot (Praha, Brno, Ostrava, …)
- **Hierarchická dimenze**: hodnoty organizované do stromu úrovní

```
Kontinent
  └── Země
        └── Územní celek
              └── Město
```

```
Rok
  └── Kvartál
        └── Měsíc
              └── Týden
```

---

# Definice multidimenzionální kostky

- Nechť existuje uspořádaná množina **n dimenzí** $\{D_1, D_2, D_3, \dots, D_n\}$
- **Multidimenzionální kostka** je funkce:

  $$g_m(A_1 \times A_2 \times A_3 \times \dots \times A_m) = F$$

  kde $\{A_1, A_2, \dots, A_m\}$ je **uspořádaná podmnožina aktivních dimenzí** ($m \leq n$)

- Prvky $F$ nazýváme **fakty (míry, _measures_)**

---

# Fakt (míra, measure)

- **Fakt** je libovolná **agregovatelná** hodnota (lze ji sčítat, průměrovat, apod.)
- Příklady faktů:
    - Počet prodaných kusů
    - Tržba v Kč
    - Průměrná cena
- Výsledkem jsou kostky _počtů_, _součtů_, _průměrů_ apod.
- Fakta jsou organizována na průsečících hodnot dimenzí

---

# 3D kostka – příklad

- Dimenze: **čas** × **produkt** × **region**
- Na každém průsečíku je uložen (nebo vypočten) **fakt** – např. objem prodejů

```
                    ┌──────────────────┐
                   /                  /│
                  /     Produkt       / │
                 /                  /  │
                └──────────────────┘   │
        Region  │                  │   │
                │     fakt         │  /
                │                  │ /   Čas
                └──────────────────┘
```

---

# Podkostky (kuboidy)

- Z n-dimenzionální kostky lze odvozovat **podkostky** (kuboidy) – kostky s méně dimenzemi
- Podkostka vznikne **agregací** přes jednu nebo více dimenzí (roll-up)
- Podkostky tvoří **částečně uspořádanou množinu (poset)**:

  $$g(A_1 \times \dots \times A_i \times \dots \times A_m) \leq g(A_1 \times \dots \times A_{m-1})$$

  Podkostka je „větší", pokud má o jednu dimenzi méně

---

# Kostka jako svaz kuboidů

- Množina všech podkostek jedné kostky tvoří **svaz** (lattice)
- **Vrcholový kuboid** (0D): jediný agregovaný fakt přes _všechny_ dimenze (`all`)
- **Základní kuboid** (nD): fakta pro _všechny_ aktivní dimenze

Příklad pro 4 dimenze (time, item, location, supplier):

```
               all
          /  |  |  \
       time item loc sup       ← 1D kuboidy
        / \ / \ / \ / \
    time,item  time,loc  ...   ← 2D kuboidy
           ...
    time, item, location, supplier ← základní 4D kuboid
```

---

# Multidimenzionální kostka jako řídká matice

- Každá dimenze $A_i$ má **skutečnou kardinalitu** $k_i$ (skutečný počet prvků)
- Výsledná kostka je **„vykotlaná" – řídká n-rozměrná matice**
    - Ne všechny průsečíky dimenzí mají definovanou hodnotu faktu
- Příklad: ne pro každou kombinaci (den, produkt, obchod) existuje prodej

<!-- POZNÁMKA: Následující slajdy s formálním matematickým aparátem (Hasseův diagram,
     definice svazu, průsek, spojení) jsou z původní přednášky. Zvažte jejich
     vypuštění nebo přesunutí do přílohy – pro praktické pochopení BI nejsou nutné. -->
