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
	- Např.
http://noviny.cz/clanky.xml
http://noviny.cz/clanky.json
	- Využití MIME pro rozlišení typu, HTTP content negotiation

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
	- Neřešíme - je vždy součástí aplikačního serveru

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

- Demo: [endpointy](https://github.com/DIFS-Teaching/jakartaee-basic/tree/main/rest-api/src/main/java/cz/vut/fit/pis/api)

---

# Konfigurace
- Třída odvozená od `javax.ws.rs.core.Application`
- Konfigurace pomocí anotací

- Např. [ApplicationConfig](https://github.com/DIFS-Teaching/jakartaee-basic/blob/main/rest-api/src/main/java/cz/vut/fit/pis/api/ApplicationConfig.java)

---

# Klientská aplikace
- Zasílání REST požadavků
	- Jednotlivé JS frameworky mají vlastní infrastrukturu
- Prezentační logika
	- Navigace
	- Přechody mezi stránkami
	- Výpisy chyb, apod.
- Viz např. [jednoduchý JS klient](https://github.com/DIFS-Teaching/jakartaee-basic/blob/main/rest-api/src/main/webapp/client.html)

---

# Návrh REST rozhraní
- Architektura REST je volná, umožňuje ``chaoticky'' přidávat endpointy podle potřeby
- **Systematický návrh je nutný**
	- Pevné datové struktury (vycházející z doménového modelu)
		- Včetně reprezentace chybových stavů
	- Mapování business operací na endpointy (vycházející z případů použití)
- Ideálně formální popis rozhraní
	- Mnohem lepší než sdílená tabulka

---

# Popis služeb v REST
- WADL (Web Application Description Language)
	- Založený na XML
	- Podpora v Javě – např. Payara
- OpenAPI https://swagger.io/specification/ 
	- Používá YAML (alternativně JSON)
	- Např. Payara/Liberty \
http://localhost:8080/openapi/
	- Generátory rozhraní třetích stran, např. \
https://github.com/OpenAPITools 

---

# Autentizace v REST
- Protokol REST je definován jako **bezstavový**
	- Požadavek musí obsahovat vše, žádné ukládání stavu na serveru
- To teoreticky vylučuje možnost použití sessions pro autentizaci
	- Technicky to ale možné je
	- Problém např. pro mobilní klienty
- Alternativy pro autentizaci:
	- **HTTP Basic** autentizace (nutné HTTPS)
	- Použití tokenu validovatelného na serveru – např. **JWT**
	- Složitější mechanismus, např. OAuth

---

# HTTP Basic
- Standardní mechanismus HTTP, využívá speciální hlavičky
- Požadavek musí obsahovat hlavičku **Authorization**
	- Obsahuje jméno a heslo; nešifrované pouze kódované (base64)
		- **Je nutné použít HTTPS**
- Pro nesprávnou nebo chybějící autentizaci server vrací **401 Auhtorization Required**
	- V hlavičce `WWW-Autenticate` je identifikace oblasti přihlášení
	- Klient tedy zjistí, že je nutná autentizace pro tuto oblast

---

# JSON Web Token (JWT)
- Řetězec složený ze 3 částí
	- Header (hlavička) – účel, použité algoritmy (JSON)
	- Payload (obsah) – JSON data obsahující id uživatele, jehopráva, expiraci apod.
	- Signature (podpis) – pro ověření, že token nebyl podvržen nebo změněn cestou
- Tyto tři části se kódují (base64) a spojí do jednoho řetězce
	- **xxxxx.yyyyy.zzzzz**

---

# Použití JWT
- Klient kontaktuje **autentizační server** a dodá autentizační údaje
	- Stejný server, jaký poskytuje API, nebo i úplně jiný (např. Twitter)
- Autentizační server vygeneruje podepsaný JWT a vrátí klientovi
- Klient předá JWT při každém volání API
	- Nejčastěji opět v hlavičce: \
`Authorization: Bearer xxxxx.yyyyy.zzzzz`
	- API ověří platnost, role uživatele může být přímo v JWT

---

# JWT v Javě
- Součástí standardu Microprofile
	- Ne přímo součást Jakarta EE
	- Ale dostupná na běžných serverech (Payara, Liberty, ...)
- Lze snadno spojit s JAX-RS
- Demo: https://github.com/DIFS-Teaching/rest-auth 

---

# Generování tokenu

- Nastavení hodnot _claims_
	- Zejména `iss`, `upn` a `groups`
- Podpis privántím klíčem (RSA, ECDSA), nebo symetrická kryptografie (HMAC)
- Klient uloží token a posílá s každým požadavkem
- Postup generování klíčů [např. zde](https://docs.payara.fish/community/docs/Technical%20Documentation/MicroProfile/JWT.html#_java_ee_security_and_jwt)

---

# Autorizace pomocí JWT

- Ověření podpisu pomocí veřejného klíče
- Ověření vydavatele (`iss`)
- Použití uživatelského jména (`upn`) a rolí (`groups`) pro autorizaci.

---

# Autorizace v Javě

- Zapnutí pro celou aplikaci + ověření role u endpointu

```java
@ApplicationPath("resources")
@LoginConfig(authMethod = "MP-JWT")
@DeclareRoles({ "admin", "staff", "customer" })
public class JAXRSConfiguration extends Application {

}
```
```java
@GET
@Path("/protected")
@RolesAllowed("admin")
public String getProtected() {
	return "ok";
}
```
---

# Konfigurace JWT

- Pomocí Java properties, např. soubor \
`META-INF/microprofile-config.properties`

```properties
mp.jwt.verify.publickey.location=/publicKey.pem
mp.jwt.verify.issuer=fitdemo
```

(přepokládá veřejný klíč v `/publicKey.pem`)
