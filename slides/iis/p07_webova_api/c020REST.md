<!-- .slide: class="section" -->

<header>
	<h1>REST</h1>
	<p>Nejjednodušší cesta k webovému API</p>
</header>

---

# REST

- Předpokládá CRUD (Create-Retrieve-Update-Delete) operace s *entitami*
	- Ale ve skutečnosti přistupujeme k business vrstvě, ne přímo k datům!
	- Tzn. voláme aplikační logiku
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

# Návrh REST rozhraní

- Architektura REST je volná, umožňuje ``chaoticky'' přidávat endpointy podle potřeby
- **Systematický návrh je nutný**
	- Pevné datové struktury (vycházející z doménového modelu)
		- Včetně reprezentace chybových stavů
	- Mapování business operací na endpointy (vycházející z případů použití)
- **Ideálně formální popis rozhraní**
	- Mnohem lepší než sdílená tabulka

---

# OpenAPI

- Strukturovaný popis REST rozhraní v YAML nebo JSON\
	https://swagger.io/specification/ 
- Generátory rozhraní v cílových jazycích, např. \
	https://github.com/OpenAPITools 
- Generování dokumentace \
	[Popis rozhraní](https://fitlayout.github.io/restapi/openapi.yaml) --
	[HTML dokumentace](https://fitlayout.github.io/restapi/)
- Popis rozhraní je možno generovat automatizovaně
	- Např. z implementace API v Javě
