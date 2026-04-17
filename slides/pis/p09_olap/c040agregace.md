<!-- .slide: class="section" -->

<header>
	<h1>Agregace</h1>
	<p>Agregační funkce a výpočet podkostek</p>
</header>

---

# Agregační funkce

- **Agregační funkce** shlukují množiny hodnot do jediné hodnoty
- Základní agregační funkce:
    - **Počet** (COUNT)
    - **Součet** (SUM)
    - **Průměr** (AVG)
    - **Maximum** (MAX)
    - **Minimum** (MIN)
- Méně časté:
    - **Medián** – prostřední hodnota uspořádané datové množiny
    - **Modus** – hodnota, která se v množině vyskytuje nejčastěji

---

# Detailní hodnoty

- **Detail** (základní fakt) je existující hodnota na průsečíku hodnot všech dimenzí $(d_1, d_2, \dots, d_n)$
- Příklad tabulky detailních prodejů (time × item × location):

| time | item   | location | fakt |
|------|--------|----------|------|
| 22.6 | rohlík | Praha    | 6    |
| 22.6 | rohlík | Brno     | 12   |
| 22.6 | rohlík | Brno     | 4    |
| 22.6 | párek  | Brno     | 9    |
| 22.6 | párek  | Praha    | 21   |
| 23.6 | rohlík | Brno     | 5    |
| 23.6 | rohlík | Praha    | 14   |
| …    | …      | …        | …    |

Pro stejné hodnoty dimenzí může existovat více faktů (např. více transakcí).

---

# Výpočet podkostky – 1. krok

- Nejprve agregujeme detailní hodnoty se **stejnými hodnotami dimenzí**

| time | item   | location | fakt (součet) |
|------|--------|----------|---------------|
| 22.6 | rohlík | Praha    | 22            |
| 22.6 | rohlík | Brno     | **19**        |
| 22.6 | párek  | Brno     | **13**        |
| 22.6 | párek  | Praha    | 21            |
| 23.6 | rohlík | Praha    | 14            |
| 23.6 | rohlík | Brno     | 5             |

Celkový součet: **94** (nemění se)

---

# Podkostka bez dimenze location

- Agregujeme přes dimenzi _location_:

| time | item   | fakt (součet) |
|------|--------|---------------|
| 22.6 | rohlík | **41**        |
| 22.6 | párek  | **34**        |
| 23.6 | rohlík | **19**        |

Celkový součet: **94**

---

# Podkostka bez dimenze item

| time | fakt (součet) |
|------|---------------|
| 22.6 | **75**        |
| 23.6 | **19**        |

Celkový součet: **94**

---

# Vrcholový kuboid (0D)

- Agregace přes _všechny_ dimenze:

| fakt |
|------|
| **94** |

- Jediný agregovaný fakt – celkový součet přes vše.

---

# Formální definice podkostek

- Pro dané uspořádání $n$ dimenzí $\{D_1, D_2, \dots, D_n\}$ platí pro podkostky
  $\textbf{součet}_m$, $\textbf{počet}_m$, $\textbf{průměr}_m$ a jejich přímé předchůdce $(m+1)$:

$$\textbf{součet}_m(d_1, \dots, d_m) = \sum_{d_i \in D_i} \textbf{součet}_{m+1}(d_1, \dots, d_i, \dots, d_m)$$

$$\textbf{počet}_m(d_1, \dots, d_m) = \sum_{d_i \in D_i} \textbf{počet}_{m+1}(d_1, \dots, d_i, \dots, d_m)$$

$$\textbf{průměr}_m = \textbf{součet}_m \,/\, \textbf{počet}_m$$

<!-- POZNÁMKA: Tato sekce je poměrně formální. Záleží na cílové skupině, zda ji
     zachovat nebo nahradit jednoduchým slovním popisem a příkladem. -->
