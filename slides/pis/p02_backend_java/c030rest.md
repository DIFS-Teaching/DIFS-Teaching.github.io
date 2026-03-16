<!-- .slide: class="section" -->

<header>
	<h1>Webové API</h1>
	<p>REST rozhraní pomocí JAX-RS</p>
</header>

---

# REST

- Předpokládá CRUD (Create-Retrieve-Update-Delete) operace s *entitami*
	- Ale ve skutečnosti přistupujeme k **business vrstvě**, ne přímo k datům!
	- Tzn. **voláme aplikační logiku**
- Úzká vazba na HTTP
	- Využití HTTP metod a jejich významu
	- Využití stavových kódů v HTTP
- Nedefinuje formát přenosu dat, obvykle JSON, méně XML (často obojí)

---

# Endpointy

- Endpoint = URL, na které lze zaslat požadavek
- Reprezentuje **zdroj** (_resource_), který má nějaký **stav** (_state_)
- Endpointy pro operace se zdroji
	- Kolekce entit, např. `http://obchod.cz/api/objednavky`
	- Jedna entita, např. `http://obchod.cz/api/objednavky/8235`
- Endpointy pro volání funkcí
	- Např. `http://obchod.cz/api/odesli-objednavku`

---

# Metody HTTP -- Operace se zdroji

- **GET**
	- Čtení stavu zdroje (read)
- **POST**
	- Přidání podřízeného zdroje (přidání do kolekce, create)
- **PUT**
	- Nahrazení zdroje novým stavem (update)
- **PATCH**
	- Nahrazení části zdroje (update)
- **DELETE**
	- Smazání zdroje (delete)

---

# Metody HTTP -- Volání funkcí

- **GET** i **POST**
	- Vykoná operaci vrátí výsledek (serializovaná data)
- Pokud je výsledkem operace nový zdroj, jeho URL se vrátí v hlavičce `Location`.

---

# Stavový kód

- Stavový kód odpovědi HTTP může odpovídat výsledku operace
- Typicky například:
	- 200 Ok
	- 201 Created
	- 400 Bad request
	- 403 Forbidden
	- 404 Not found
	- 500 Internal server error

---

# Formát přenosu dat
- Není specifikován, záleží na službě
	- Obvykle JSON nebo XML (schéma záleží na aplikaci)
- Často více formátu k dispozici
	- Využití MIME pro rozlišení typu, HTTP content negotiation \
	(hlavička `Accept:`)

---

# REST a Jakarta EE
- JAX-RS API součástí standardu
- Vytvoření služeb pomocí anotací
- Aplikační server zajistí funkci endpointu (JAX-RS servlet)
	- Mapování URL a HTTP metod na Javovské objekty a metody
	- Serializace a deserializace JSON/XML na objekty
- Různé implementace
	- JAX-RS – Jersey (Glassfish), Apache Axis
	- Serializace – Jackson, gson, MOXy, …
	- Neřešíme – je vždy součástí aplikačního serveru

---

# REST v Javě

```java
import javax.ws.rs.GET;
import javax.ws.rs.Produces;
import javax.ws.rs.Path;

@Path("/users/{username}")
public class UserResource {

    @GET
    @Produces("text/xml")
    public User getUser(@PathParam("username") String userName) {
        // volání business operací (aplikační logika)
	    return someUser;
    }
}
```

- Definované typy pro přenos dat -- **Data Transfer Objects (DTO)**
- Jednoduchý příklad: [ping endpoint](https://github.com/DIFS-Teaching/jakartaee-starter/blob/main/src/main/java/cz/vut/fit/pis/start/rest/PingEndpoint.java)

---

# Konfigurace
- Třída odvozená od `javax.ws.rs.core.Application`
- Konfigurace pomocí anotací

- Např. [ApplicationConfig](https://github.com/DIFS-Teaching/jakartaee-starter/blob/main/src/main/java/cz/vut/fit/pis/start/rest/ApplicationConfig.java)
