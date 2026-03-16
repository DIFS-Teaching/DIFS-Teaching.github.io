<!-- .slide: class="section" -->

<header>
	<h1>Business vrstva</h1>
	<p>Implementace aplikační logiky</p>
</header>

---

# Enterprise Java Beans (EJB)
- Zapouzdřují business logiku aplikace
- Poskytují business operace – definované rozhraní (metody)
- EJB kontejner zajišťuje další služby
	- Dependency injection
	- Transakční zpracování
		- Metoda obvykle tvoří transakci, není-li nastaveno jinak

---

# Vytvoření EJB
- Instance vytváří a spravuje EJB kontejner
- Vytvoření pomocí anotace třídy
	- `@Stateless` – bezstavový bean
		- Efektivnější správa – pool objektů přidělovaných klientům
	- `@Stateful` – udržuje se stav
		- Jedna instance na klienta
	- `@Singleton`
		- Jedna instance na celou aplikaci
- Použití (získání instance)
	- Anotace `@EJB`

---

# Contexts and Dependency Injection (CDI)
- Obecný mechanismus pro DI mimo EJB
- Omezuje závislosti mezi třídami přímo v kódu
	- Flexibilita (výměna implementace), lepší testování, …
- Injektovatelné objekty
	- Třídy, které nejsou EJB
	- Různé vlastnosti pomocí anotací
- Použití objektu
	- Anotace `@Inject`
	- CDI kontejner zajistí získáni a dodání instance

---

# CDI – Injektovatelné objekty
- Téměř jakákoliv Javovská třída
- Scope
	- `@Dependent` – vzniká pro konkrétní případ, zaniká s vlastníkem (default)
	- `@RequestScoped` – trvá po dobu HTTP požadavku
	- `@SessionScoped` – trvá po dobu HTTP session
	- `@ApplicationScoped` – jedna instance pro aplikaci
	- _Pozor na shodu jmen se staršími anotacemi JSF_
- Pokud má být přístupný z GUI (pomocí EL)
	- Anotace `@Named`

