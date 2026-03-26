<!-- .slide: class="section" -->

<header>
	<h1>Transakční zpracování</h1>
	<p>Opakování a rozšíření — ACID, modely transakcí</p>
</header>

---

# ACID — přehled

| Vlastnost | Význam | Kdo zajišťuje |
|-----------|--------|---------------|
| **A** – Atomičnost | Celá transakce, nebo nic; commit / rollback | TPS |
| **C** – Konzistence | DB splňuje IO před i po transakci | **Programátor** |
| **I** – Izolovanost | Souběžné provádění = sekvenční výsledek; úrovně: serializable → repeatable read → read committed → read uncommitted | TPS |
| **D** – Trvanlivost | Potvrzené změny přežijí havárii; žurnál, zrcadlení | TPS |

---

# Kdo co zajišťuje
- **Programátor** zodpovídá za konzistenci transakce — správně sestavit operace tak, aby DB přešla z jednoho konzistentního stavu do druhého
- **TPS** zajišťuje automaticky:
	- **Atomičnost** – mechanismus commit/rollback
	- **Izolovanost** – zamykání záznamů, uspořadatelné plány
	- **Trvanlivost** – žurnál (write-ahead log), zrcadlení

*Celý zbytek přednášky se zabývá modely, kde se záměrně od ACID odchylujeme — vždy je důležité vědět, která vlastnost se porušuje a proč.*

---

# Důvody zrušení transakce

**Nepředvídatelné:**
- havárie systému

**V režii TPS:**
- porušení integritního omezení
- porušení izolovanosti souběžných transakcí
- detekované uváznutí (deadlock)

**V režii transakce / programátora:**
- na požadavek samotné transakce (`rollback`)
