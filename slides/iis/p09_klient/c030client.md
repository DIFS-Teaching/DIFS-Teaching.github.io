<!-- .slide: class="section" -->

<header>
    <h1>Klientské programování</h1>
    <p>REST klient v JavaScriptu, kdysi též AJAX</p>
</header>

---

# Co potřebujeme

-   HTML + CSS
    -   implementace a design stránky
-   DOM
    -   změny v dokumentu
-   JSON (případně XML, ...)
    -   výměna dat
-   JavaScript
    -   logika UI
-   `fetch()` (dříve `XMLHttpRequest`)
    -   JS API v prohlížeči pro odesílání požadavků

---

# Přenášená data

-   Strukturovaná data přes HTTP
    -   Je třeba _serializace_
    -   XML (původně)
    -   JSON (dnes převažuje)
-   Části stránky
    -   Obvykle přímo útržky HTML

---

# Odesílání dat

<div class="small">

-   V rámci GET požadavku lze odesílat hodnoty parametrů
    -   Standardně klíč-hodnota  
        `https://example.com/articles/?cat=business&id=4827`
    -   Nějaká konvence zakódování do URL, server musí dekódovat  
        `https://example.com/articles/business/4827`
-   V rámci POST, PUT, PATCH lze v těle odeslat libovolná data, je nutno specifikovat MIME typ (hlavička `Content-Type` v požadavku)
    -   `application/x-www-form-urlencoded` – jen dvojice klíč-hodnota
    -   `multipart/form-data` – dvojice klíč-hodnota a soubory
    -   `application/json`, `application/xml`, apod. – přímo serializované strukturované hodnoty
-   GET a DELETE obvykle tělo nemají (jeho význam není definován)

</div>

---

# Příjem dat

-   Výsledkem požadavku je obvykle odpověď obsahující _serializovaná data_
-   Formát serializace je indikován hlavičkou `Content-Type` v odpovědi
    -   Obvykle opět `application/json` nebo `application/xml`
-   Je zvykem, že klient uvede preferovaný formát (i více) pomocí hlavičky `Accept` v požadavku
    -   Např. `Accept: application/json`
-   Server v rámci svých možností vyhoví, případně vrátí chybu `406 Not Acceptable`

---

# Stavové kódy z pohledu klienta

-   Stavový kód indikuje výsledek operace (viz _webová API_)
-   `2xx` – úspěch: zobrazit výsledek
    -   `200 OK`, `201 Created`, `204 No Content` (žádná data)
-   `4xx` – chyba klienta: informovat uživatele
    -   `400 Bad Request`, `422 Unprocessable Content` – chybná data (zvýraznit ve formuláři)
    -   `401 Unauthorized` – chybí přihlášení (přesměrovat na přihlášení)
    -   `403 Forbidden` – přihlášen, ale nemá oprávnění
    -   `404 Not Found`, `409 Conflict`
-   `5xx` – chyba serveru: obecné chybové hlášení, případně opakovat později
-   Tělo odpovědi stále může obsahovat data (např. podrobnosti o chybě)

---

# Server

-   Implementuje _business logiku_ (operace)
-   Poskytuje REST API
    -   Každý **zdroj** (_resource_) má svoje URL (případně parametrizovatelné)
    -   Operace se zdrojem je určena HTTP metodou
-   Libovolná serverová platforma
    -   Java, .NET, PHP, Python, Node.js, ...
    -   Typicky podporováno v různých frameworcích
-   Jednoduchý příklad:
    -   [php-rest-db](https://github.com/DIFS-Teaching/basic-demos/tree/master/php-rest-db) (viz předchozí přednášky)

---

# Klient

-   Interakce s uživatelem
    -   Zobrazuje data
    -   Poskytuje rozhraní pro spouštění business operací a vstup dat
-   Volá metody API
    -   Vysílá příslušné HTTP požadavky na endpoint URL
-   Zobrazuje výsledky volání
    -   Včetně chybových stavů

---

# Klient v JavaScriptu (starý)

-   Rozhraní `XMLHttpRequest`

```JavaScript
var xhr = new XMLHttpRequest();
xhr.onreadystatechange = function() {
    if (xhr.readyState == 4 && xhr.status == 200) {
        console.log("Response received: " + xhr.responseText);
    }
}
xhr.open("POST", "post-handler.php", true);
xhr.setRequestHeader("Content-Type", "application/json");
xhr.send(JSON.stringify(data));
```

---

# Klient pomocí fetch()

```JavaScript
fetch('https://example.com/profile', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(data),
})
.then(response => response.json())
.then(result => console.log('Success:', result))
.catch(error => console.error('Error:', error));
```

-   Funkce `fetch()` vrací `Promise`, výsledek se zpracuje asynchronně

---

# Klient pomocí fetch() a await

```JavaScript
async function saveProfile(data) {
    const response = await fetch('https://example.com/profile', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(data),
    });
    if (!response.ok) {
        throw new Error(`HTTP ${response.status}`);
    }
    return await response.json();
}
```

-   Volající ošetří případnou výjimku pomocí `try` / `catch`
-   [Příklad klienta](https://github.com/DIFS-Teaching/basic-demos/blob/master/php-rest-db/client.html)

---

# Pozor na chyby

-   `fetch()` selže (vyhodí výjimku) **pouze při síťové chybě**
    -   Nedostupný server, chyba DNS, zablokování politikou CORS, ...
-   Odpověď s chybovým stavovým kódem (`4xx`, `5xx`) je z pohledu `fetch()` úspěch
    -   Je nutné testovat `response.ok` nebo `response.status`
-   Odpověď nemusí být JSON (např. chybová HTML stránka serveru)
    -   `response.json()` pak vyhodí výjimku
-   Uživatel by měl vždy dostat srozumitelnou informaci o chybě

---

# Zobrazení dat v DOM

```JavaScript
const persons = await response.json();
const list = document.querySelector('#persons');
list.replaceChildren();                  // odstranit původní obsah
for (const p of persons) {
    const li = document.createElement('li');
    li.textContent = `${p.name} ${p.surname}`;
    list.append(li);
}
```

-   `textContent` vkládá data jako text – bezpečné
-   `innerHTML` s daty ze serveru = riziko **XSS**
    -   Data mohou obsahovat HTML značky včetně `<script>`, apod.
-   Dříve se pro tyto úlohy používala knihovna _jQuery_ – dnes nahrazena standardními API

---

# Same-origin policy

-   Bezpečnostní omezení v prohlížečích
-   Skript smí číst odpovědi jen ze zdrojů se stejným _origin_, jako má **stránka**, ve které běží
    -   Origin = schéma + hostname + port
    -   Rozhoduje origin dokumentu, ne URL, odkud byl skript načten
-   Pozor: omezení se týká **čtení odpovědi**
    -   Jednoduché požadavky (např. odeslání formuláře) prohlížeč odešle i na jiný origin
    -   Proto existuje útok _CSRF_
-   Jde o ochranu uživatele v prohlížeči, ne o ochranu API
    -   Jiní klienti (`curl`, mobilní aplikace, ...) omezení nemají

---

# Cross-Origin Resource Sharing (CORS)

-   Server může omezení pro své zdroje rozvolnit pomocí hlaviček odpovědi
    -   `Access-Control-Allow-Origin: https://app.example.com`
    -   `Access-Control-Allow-Origin: *` – vhodné jen pro veřejná API
-   **Preflight** požadavek
    -   U „nejednoduchých“ požadavků (např. `PUT`, `DELETE`, JSON tělo, vlastní hlavičky)
    -   Prohlížeč nejprve pošle `OPTIONS`, server musí povolit metody a hlavičky
-   Posílání cookies na jiný origin
    -   Klient: `fetch(url, { credentials: 'include' })`
    -   Server: `Access-Control-Allow-Credentials: true` (nelze s `*`)

---

# REST API s autentizací

-   Protokol REST je definován jako _bezstavový_
    -   Požadavek musí obsahovat vše, žádné ukládání stavu na serveru
-   To teoreticky vylučuje použití sessions pro autentizaci
    -   Pro webového klienta na stejné doméně to ale technicky možné je
    -   Cookies jsou vázané na doménu a prohlížeč – komplikace pro API na jiné doméně a pro klienty mimo prohlížeč
-   Alternativy pro autentizaci:
    -   HTTP Basic autentizace (nutné HTTPS)
    -   API klíč – pro komunikaci mezi servery
    -   Token validovatelný na serveru – např. JWT
    -   Delegovaný přístup a externí přihlášení – OAuth 2, OIDC

---

# HTTP Basic

-   Standardní mechanismus HTTP, využívá speciální hlavičky
-   Požadavek musí obsahovat hlavičku `Authorization`
    -   `Authorization: Basic dXNlcjpoZXNsbw==`
    -   Obsahuje jméno a heslo; nešifrované, pouze kódované (base64)
        -   **Je nutné použít HTTPS**
-   Pro nesprávnou nebo chybějící autentizaci server vrací `401 Unauthorized`
-   Heslo se posílá s každým požadavkem – vhodné spíš pro jednoduchá a interní API

---

# HTTP Basic v PHP

```php
if (!isset($_SERVER['PHP_AUTH_USER'])) {
    header('WWW-Authenticate: Basic realm="My Realm"');
    http_response_code(401);
    echo 'Authentication required';
    exit;
}
$user = $_SERVER['PHP_AUTH_USER'];
$password = $_SERVER['PHP_AUTH_PW'];
// ověření jména a hesla (např. password_verify() proti DB) ...
```

-   Při provozu přes PHP-FPM / CGI je nutné, aby HTTP server hlavičku `Authorization` předal PHP
    -   Např. Apache: `CGIPassAuth On`

---

# JSON Web Token (JWT)

-   Řetězec složený ze 3 částí
    1.  Header (hlavička) – typ tokenu, použitý algoritmus podpisu (JSON)
    2.  Payload (obsah) – JSON data obsahující id uživatele, jeho práva, expiraci apod.
    3.  Signature (podpis) – pro ověření, že token nebyl podvržen nebo změněn
-   Tyto tři části se kódují (base64url) a spojí do jednoho řetězce
    -   `xxxxx.yyyyy.zzzzz`
-   Obsah je pouze podepsaný, **není šifrovaný** – může ho přečíst kdokoliv
    -   Nevkládat citlivé údaje
-   Podpis: sdílený klíč (HMAC, `HS256`) nebo asymetrický (`RS256`, `ES256`)

---

# Použití JWT pro autentizaci

1.  Klient kontaktuje _autentizační server_ a dodá autentizační údaje
    -   Stejný server, jaký poskytuje API, nebo i úplně jiný (např. Google, Microsoft, Keycloak, univerzitní SSO)
2.  Autentizační server vygeneruje podepsaný JWT a vrátí klientovi
3.  Klient předá JWT při každém volání API
    -   Nejčastěji opět v hlavičce:  
        `Authorization: Bearer xxxxx.yyyyy.zzzzz`
    -   API ověří podpis a expiraci, role uživatele může být přímo v JWT
-   Platný token nelze snadno odvolat
    -   Krátká platnost (minuty) + _refresh token_ pro získání nového

---

# Kam uložit token v prohlížeči?

-   `localStorage` / `sessionStorage`
    -   Jednoduché, token se přidává do hlavičky `Authorization` ručně
    -   Při **XSS** může útočník token přečíst a odcizit
-   Cookie s atributy `HttpOnly`, `Secure`, `SameSite`
    -   JavaScript k ní nemá přístup, prohlížeč ji posílá automaticky
    -   Je nutné řešit _CSRF_ (`SameSite`, CSRF token)

---

# OAuth 2 a OpenID Connect

-   **OAuth 2** – delegovaný přístup aplikace k API cizí služby
    -   Uživatel aplikaci povolí přístup ke svým datům, aniž by jí sdělil heslo
    -   Např. tiskárna fotografií získá přístup k fotkám uživatele v cloudové službě
    -   Aplikace dostane přístupový token (často JWT) a posílá ho v hlavičce `Authorization`
-   **OpenID Connect** (OIDC) – přihlášení uživatele pomocí externího poskytovatele identity
    -   Nadstavba OAuth 2, aplikace se dozví, kdo je uživatel
    -   Např. „Přihlásit přes Google“, jednotné přihlášení (SSO) v organizaci
-   Podrobněji viz předmět _PIS_

---

# Implementace klienta – alternativy

-   Čistý JavaScript (`fetch()` + DOM) – pro jednoduché aplikace
-   _jQuery_ – dříve velmi rozšířené, dnes již pro nové projekty spíše nevhodné
-   React
    -   Knihovna pro tvorbu UI, komponenty, virtuální DOM, rozšíření syntaxe (JSX)
    -   Obvykle s frameworkem, např. _Next.js_
-   Vue.js, Svelte
    -   Jednodušší začátek, Svelte bez virtuálního DOM (kompilátor)
-   Angular
    -   Komplexní framework, TypeScript, vhodný pro rozsáhlé aplikace

---

# Shrnutí

-   JavaScript umožňuje tvorbu komplexních klientských aplikací s robustním GUI
-   Umožňuje oddělit business logiku (na serveru) od prezentační logiky (na klientovi)
-   Základem je `fetch()` + práce s DOM, pozor na ošetření chyb a XSS
-   Prohlížeč omezuje přístup k jiným originům, server může povolit pomocí CORS
-   Autentizace: session cookie, tokeny (JWT), OAuth 2 / OpenID Connect
-   Pro rozsáhlé aplikace existuje řada frameworků
