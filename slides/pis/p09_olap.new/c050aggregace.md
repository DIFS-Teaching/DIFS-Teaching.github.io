<!-- .slide: class="section" -->

<header>
	<h1>Agregace</h1>
	<p>Agregační funkce a výpočet kostek</p>
</header>

---

# Agregační funkce

- Shlukují množiny (obvykle číselných) hodnot do **jediné hodnoty**
- Základní agregační funkce:
	- **Počet** (COUNT)
	- **Součet** (SUM)
	- **Minimum** (MIN), **Maximum** (MAX)
	- **Aritmetický průměr** (AVG)
- Rozšířené:
	- **Medián** – prostřední hodnota uspořádané datové množiny
	- **Modus** – hodnota vyskytující se v množině nejčastěji

---

# Typy agregačních výpočtů

- **Distributivní**: výsledek lze spočítat z dílčích výsledků
	- Příklady: COUNT, SUM, MIN, MAX
	- Celkový součet = součet dílčích součtů ✓

- **Algebraické**: výsledek funkce s _M_ parametry, z nichž každý vzniká distributivní funkcí
	- Příklady: průměr (SUM/COUNT), variance
	- Celkový průměr ≠ průměr dílčích průměrů (pokud se liší počty vzorků)

- **Holistické**: neexistuje algebraické vyjádření z dílčích výsledků
	- Příklady: medián, modus, nejčastěji se vyskytující položka

---

# Proč průměr není distributivní

- Platí to **pouze při stejném počtu vzorků** v obou skupinách
- Příklad (různé počty vzorků):
	- {1, 2, 3, 4, 5, 6}: průměr = **3,5**
	- {100, 200, 300}: průměr = **200**
	- Průměr průměrů: (3,5 + 200) / 2 = **101,75**
	- Celkový průměr: 621 / 9 = **69** ✗

---

# Výpočet agregátů – první krok

- Pro _n_-dimenzionální kostku se nejprve agregují detailní hodnoty se stejnými hodnotami dimenzí do jediného záznamu:
	- součet_n(d₁, …, dₙ) = Σ všech detailních hodnot s danými dimenzemi
	- počet_n(d₁, …, dₙ) = počet detailních záznamů
	- průměr_n = součet_n / počet_n

---

# Výpočet podkostek

- Pro podkostku s _m_ < _n_ dimenzemi se agregují hodnoty přes odstraněnou dimenzi _Dᵢ_:
	- součet_m(d₁, …, dₘ) = Σ součet_{m+1} přes všechny hodnoty z _Dᵢ_
	- počet_m(d₁, …, dₘ) = Σ počet_{m+1} přes všechny hodnoty z _Dᵢ_
	- průměr_m = součet_m / počet_m

---

# Příklad výpočtu – detailní hodnoty

| time | item | location | fakt |
|------|------|----------|------|
| 22.6. | rohlík | Praha | 16 |
| 22.6. | rohlík | Brno | 19 |
| 22.6. | párek | Praha | 21 |
| 22.6. | párek | Brno | 13 |
| 23.6. | rohlík | Praha | 14 |
| 23.6. | rohlík | Brno | 5 |
| **celkem** | | | **88** |

---

# Příklad – podkostka bez dimenze location

| time | item | součet |
|------|------|--------|
| 22.6. | rohlík | 35 |
| 22.6. | párek | 34 |
| 23.6. | rohlík | 19 |
| **celkem** | | **88** |

---

# Příklad – podkostka bez dimenzí item a location

| time | součet |
|------|--------|
| 22.6. | 69 |
| 23.6. | 19 |
| **celkem** | **88** |

---

# Materializace datové kostky

- **Materializace** = vypočtení agregačních hodnot **předem** a jejich uložení
- Druhy materializace:
	- **Plná materializace** – uložení všech kuboidů (rychlé dotazy, velké nároky na prostor)
	- **Bez materializace** – vše se počítá za běhu (pomalé dotazy)
	- **Částečná materializace** – výběr kuboidů na základě velikosti, frekvence přístupů nebo sdílení
- Výběr kuboidů k materializaci = klíčový optimalizační problém
