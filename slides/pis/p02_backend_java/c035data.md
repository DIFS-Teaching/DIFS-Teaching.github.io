<!-- .slide: class="section" -->

<header>
	<h1>Persistence dat</h1>
	<p>Objektové rozhraní JPA</p>
</header>

---

# Java Bean

```java
public class Person
{
    private long id;
    private String name;
    private String surname;
    private Date born;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

	…

}
```

---

# Java Bean - role

- POJO -- Plain old Java object
- Data Transfer Object (DTO)
	- Pro přenos (HTTP) -- serializace a deserializace
- Entita (Entity)
	- Pro ukládání do databáze -- persistenci

---

# Persistence
- Pomocí anotací vytvoříme z třídy **entitu** persistence

```java
@Entity
@Table(name = "person")
public class Person

{
    @Id
    private long id;
    private String name;
    private String surname;
    private Date born;

	...
}
```

- Více v další přednášce

---

# Konfigurace databáze

- V režii aplikačního serveru
	- Server poskytuje aplikaci připojení k databázi
	- To umožňuje různé konfigurace (produkční/vývojové prostředí) bez zásahů do aplikace
- Vrstvy implementace
	1. Relační DB server + JDBC ovladač
	2. JDBC zdroj: Nakonfigurované připojení ke konkrétní databázi (vč. přístupových údajů)
	3. Abstraktní vrstva - např. O/R mapování využívající JDBC zdroj

---

# Databázová konektivita
- Konfigurace zdroje dat (JDBC data source)
	- Ovladač, adresa serveru, databáze, přihlašovací údaje
	- Přiřazené jméno (např. `jdbc/demo`) 
- Aplikace následně využívá definovaný zdroj daného jména
	- Přenositelnost aplikaci do různých prostředí

---

# Konfigurace -- Open Liberty

- Pro ``velký'' server
	- `wlp/usr/servers/<nazev>/server.xml`
	- Definice ovladačů i datového zdroje
- Pro aplikaci
	- `src/main/liberty/config/server.xml` 
	- Příklad [knihovny](https://github.com/DIFS-Teaching/jakartaee-basic/blob/main/web-frontend/pom.xml), [konfigurace zdroje](https://github.com/DIFS-Teaching/jakartaee-basic/blob/main/web-frontend/src/main/liberty/config/server.xml)

Viz [Relational database connections with JDBC](https://openliberty.io/docs/latest/relational-database-connections-JDBC.html)

---

# Konfigurace -- Payara
- Pro server
	- Webové administrační rozhraní http://localhost:4848
	- příp. nástroje příkazové řádky
	- [Using MySQL with Payara](https://blog.payara.fish/using-mysql-with-payara)
- Pro aplikaci
	- Soubor `WEB-INF/glassfish-resources.xml` 
	- Příklad: [knihovny](https://github.com/cicekhayri/payara-micro-javaee-crud-rest-starter-project/blob/master/pom.xml), [konfigurace zdroje](https://github.com/cicekhayri/payara-micro-javaee-crud-rest-starter-project/blob/master/src/main/webapp/WEB-INF/glassfish-resources.xml)

---

# Konfigurace v aplikaci

- Soubor [persistence.xml](https://github.com/DIFS-Teaching/jakartaee-basic/blob/main/rest-api/src/main/resources/META-INF/persistence.xml)
- Jméno jednotky persistence
- Odkaz na konfigurovaný *data source*
	- JNDI name (např. `jdbc/demo`)
	- Případně další parametry pro mapování
		- Např. řízení automatického generování schématu

