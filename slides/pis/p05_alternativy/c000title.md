<!-- .slide: class="title" -->

<div class="logo"></div>
<div class="main">
    <header>
        <h1>Pokročilé informační systémy</h1>
        <p class="subtitle">Alternativní tehchnologie a architektury</p>
    </header>
    <p class="author" style="margin: 0"><strong>doc. Ing. Radek Burget, Ph.D.</strong><br>
        <a href="mailto:burgetr@fit.vutbr.cz">burgetr@fit.vutbr.cz</a>
    </p>
</div>

---

# Třívrstvá architektura
- Java EE umožňuje implementovat **monolitický** IS s **třívrstvou architekturou**:
	- Databázová vrstva
		- JPA – definice entit, persistence (`PersistenceManager`)
		- Alternativně: Relační databáze (JDBC), NoSQL (MongoDB), …
	- Logická (business) vrstva
		- Enterprise Java Beans (EJB) nebo CDI beans
		- Dependency injection – volné propojení
	- Prezentační vrstva
		- Webové rozhraní (JSF) nebo API (REST, JAX-RS)
