<!-- .slide: class="section" -->

<header>
	<h1>GraphQL</h1>
	<p>Typovaná aplikační rozhraní</p>
</header>

---

 # GraphQL
- https://graphql.org/ 
- Motivace: klient (klienti) potřebují v různých situacích různá data
	- Např. stránka „seznam osob“ vs. „detail osoby“
	- REST endpoint vrací vždy stejnou strukturu
		- Redundance dat (nevyužijeme všechna data)
		- Více dotazů ((ne)efektivita, složitější logika klienta)
  - Získat některá data může být drahé (pokud je klient nepotřebuje)
- Řešení GraphQL
	- Popis datového modelu API
	- Dotaz na API specifikuje požadovaný tvar odpovědi
  - **Předvídatelný výsledek dotazu**

---

# GraphQL – datový model
- Datový model API (ne nutně serverové aplikace)
- Jednoduché datové typy: Int, Float, String, Boolean, ID, enum
- Uživatelské typy (_types_) = struktury
	- Vlastnosti (parametrizovatelné) – jméno, parametry, typ
	- Typy jednoduché, struktury (vztahy), kolekce
- Speciální typy reprezentující volání API (_root_ _types_)
	- Query – čtení dat
	- Mutation – změna dat
- GraphQL Schema Definition Language (SDL)

---

# GraphQL – definice typů

```graphql
type Person {
  name: String!
  age: Int!
  posts: [Post!]!
}
```
<!-- .element: class="col small" style="margin-top:1em;width:30%" -->

```graphql
type Car {
  type: String!
  reg: String!
  owner: Person!
}
```
<!-- .element: class="col small" style="margin-top:1em;width:30%" -->

```graphql
type Query {
  allPersons: [Person!]!
  findPerson(name: String!): Person!
}
```
<!-- .element: class="col small" style="margin-top:1em;width:80%" -->

```
type Mutation {
  createPerson(name: String!, age: Int!): Person!
}
```
<!-- .element: class="col small" style="margin-top:1em; width:80%" -->

---

# GraphQL – dotazy 

```graphql
{
  allPersons {
    name
  }
}
```
<!-- .element: class="col small" style="margin-top:1em;width:30%" -->

```json
{
  "allPersons": [
    { "name": "Jan" },
    { "name": "Karolína" },
    { "name": "Alice" }
  ]
}
```
<!-- .element: class="col small" style="margin-top:1em;width:30%" -->

```graphql
{
  findPerson(name: "James") {
    name
    age
    cars {
      type
    }
  }
}
```
<!-- .element: class="col small" style="margin-top:1em;width:30%" -->

```json
{
  "findPerson": {
    "name": "James",
    "age": 28,
    "cars": [
        { "type": "Fiat" },
        { "type": "Tesla" }
    ]
  }
}
```
<!-- .element: class="col small" style="margin-top:1em;width:30%" -->

---

# GraphQL – modifikace 

```graphql
mutation AddPerson($person: PersonInput) {
    updatePerson(p: $person) {
        id
    }
}
```
<!-- .element: class="col small" style="margin-top:1em;width:40%" -->

```json
 {
     "person": {
        "born": "1991-06-03T22:00:00Z[UTC]",
        "id": 1154731299,
        "name": "Sylvester",
        "surname": "Stalone"
     }
}
```
<!-- .element: class="col small" style="margin-top:1em;width:45%" -->

```json
{
    "data": {
        "updatePerson": {
            "id": 1154731299
        }
    }
}
```
<!-- .element: class="col small" style="margin-top:1em;width:80%" -->


---

# GraphQL přes HTTP
- Jediné endpoint URL
- Odeslání přes GET \
`http://myapi/graphql?query={me{name}}`
- Odeslání přes POST
	- Data `application/json` \
`{"query": "{me{name}}"}` \
`{"query": "{mutation ... }", "variables": {name: "Jan"}}`
	- Data `application/graphql` \
`{me{name}}`

---

# Implementace GraphQL
- Klientská strana
  - Žádná speciální podpora -- posílání POST požadavků
- Serverová strana
  - Definice datových struktur a dotazů
  - Zpracování SDL nebo generování SDL z kódu
  - Mnoho knihoven \
https://graphql.org/code/

---

# Microprofile GraphQL

- Demo: [Open Liberty Guide](https://openliberty.io/guides/microprofile-graphql.html), [demo aplikace](https://github.com/DIFS-Teaching/jakartaee-basic)
- Závislost v `pom.xml`
```xml
<dependency>
    <groupId>org.eclipse.microprofile.graphql</groupId>
    <artifactId>microprofile-graphql-api</artifactId>
    <version>2.0</version>
    <scope>provided</scope>
</dependency>        
```
- V Open Liberty přidat vlastnost na server
```xml
<feature>mpGraphQL-2.0</feature>
```

---

# Definice API

```java
@GraphQLApi
@RequestScoped
public class Api
{
    @Inject
    private PersonManager personMgr; 

    @Query
    @Description("Gets the complete list of people")
    public List<Person> getPeople()
    {
        return personMgr.findAll();
    }
}
```

---

# Definice datových typů

- Standardní java třídy (POJO)
- Volitelně lze nastavit mapování
  - jmen tříd -- `@Type("...")`
  - vlastností -- `@Name("...")`
  - a doplnit popis významu -- `@Description`.

---

# Autentizace v GraphQL

- Stejný mechanismus, jako u REST
- Stejná konfigurace JWT

```java
@GraphQLApi
@LoginConfig(authMethod = "MP-JWT", realmName = "MP-JWT")
@RequestScoped
public class Api
{
    @Inject
    private PersonManager personMgr; 

    @Query
    @RolesAllowed("admin")
    @Description("Gets the complete list of people")
    public List<Person> getPeople()
    {
        return personMgr.findAll();
    }
}
```
