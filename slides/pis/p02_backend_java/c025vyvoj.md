<!-- .slide: class="section" -->

<header>
	<h1>Praktický vývoj v Jakarta EE</h1>
	<p>Instalace a první projekt</p>
</header>

---

# Prerekvizity
- Java 17+ (21) – **musí být JDK**
	- V Linuxu v distribuci (OpenJDK)
	- Nebo např. [Adoptium](https://adoptium.net/temurin/releases/)
- Maven
	- V Linuxu v distribuci
	- Nebo např. [návod zde](https://openliberty.io/guides/maven-intro.html#installing-maven)
- Git (volitelně)
	- 100% doporučeno pro práci v týmu

---

# Komponenty
- Jakarta EE server
	- **Open Liberty** [openliberty.io](https://openliberty.io/)
	- Payara community edition [payara.fish](https://www.payara.fish/downloads/payara-platform-community-edition/)
	- TomEE, WildFly, ...
- Vývojové prostředí
	- **Eclipse** for Enterprise Java Developers
	- IntelliJ IDEA, VS Code ...
- Databázový server
	- Jakýkoliv relační ([H2](https://www.h2database.com), MySQL, ...)
- Databázový konektor (JDBC ovladač)

---

# Vývojové prostředí -- Eclipse
- Instalovat Eclipse
	- [Eclipse IDE for Enterprise Java and Web Developers](https://www.eclipse.org/downloads/packages/)
- Instalovat nástroje pro Payara a/nebo Liberty
	- Eclipse Marketplace
- Definovat server v IDE
	- Podle způsobu spouštění serveru
- Alternativy
	- VS Code, IntelliJ IDEA, ...
	- [Liberty tools](https://openliberty.io/start/#_develop_with_liberty_tools)

---

<!-- .slide: class="section" -->

<header>
	<h1>Tvorba aplikace v Jakarta EE</h1>
</header>

---

# Maven projekt
- Použití existujícího projektu
	- Např. [Jakarta EE starter](https://github.com/DIFS-Teaching/jakartaee-starter)
	- viz. `pom.xml`
- Generátory projektů
	- [Liberty start](https://openliberty.io/start/)
	- [Microprofile starter](https://start.microprofile.io/)
- Maven archetypes
	- [JakartaEE-essentials-archetype](https://github.com/AdamBien/JakartaEE-essentials-archetype)
	- [WildFly-getting-started-archetype](https://www.wildfly.org/get-started/)

---

# Vytvoření projektu v Eclipse
- Import existujícího Maven projektu [Starter project](https://github.com/DIFS-Teaching/jakartaee-starter)
	- Např. přepnout do perspektivy Git
- Update Maven projektu (Alt-F5) 
- Konfigurace později
	- Project -> Properties
		- Project Facets

---

# Maven projekt -- konfigurace
- Nastavení parametrů
	- *Project coordinates* (groupId a artifactId)
	- Packaging `war`
	- Dependencies (provided?)
- Zdrojové soubory
	- `src/main/java`
- Překlad
	- `mvn clean package`
	- Výsledný balík v `target/*.war`

---

# Struktura WAR
- Kořenový adresář je / webu
- META-INF
	- Informace o archivu
- WEB-INF/lib
	- Potřebné knihovny (*.jar)
- WEB-INF/class
	- Přeložené třídy (*.class)

---

# Java Servlet
- Třída implementující vyřizování HTTP požadavků
- Implementuje rozhraní `HttpServlet`
- Anotovaná pomocí `@WebServlet`
	- Mapování na URL

