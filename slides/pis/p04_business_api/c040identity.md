<!-- .slide: class="section" -->

<header>
	<h1>Správa identit</h1>
	<p>OAuth2, OpenID Connect, SAML</p>
</header>

---

# Správa identit v IS
- Kdo je uživatel a jaká má práva?
	- **Autentizace** – ověření identity (kdo to je?)
	- **Autorizace** – ověření oprávnění (co smí dělat?)
- Problémy centralizované správy
	- Každá aplikace spravuje vlastní uživatele → duplicita, bezpečnostní riziko
	- Uživatel si pamatuje mnoho hesel
- Řešení: **federovaná identita**
	- Identita je spravována centrálně, aplikace ji sdílejí
	- **Single Sign-On (SSO)** – přihlásíte se jednou, funguje všude

---

# Základní koncepty
- **Identity Provider (IdP)** – server, který spravuje identity a vydává tokeny
	- Příklady: Google, Facebook, Microsoft Entra ID, Keycloak
- **Service Provider / Relying Party** – aplikace, která spoléhá na IdP
- **Token** – doklad o prokázané identitě nebo oprávnění
	- Přenášen mezi stranami, ověřitelný bez dotazu na IdP
- **Claim** – tvrzení o uživateli obsažené v tokenu
	- Např. jméno, e-mail, role, organizace

---

# Přehled standardů

| Standard | Účel | Vrstva |
|----------|------|--------|
| **OAuth 2.0** | Delegovaná autorizace | Přístup ke zdrojům |
| **OpenID Connect (OIDC)** | Autentizace nad OAuth2 | Identita uživatele |
| **SAML 2.0** | Autentizace + autorizace | SSO v podnicích |
| **JWT** | Formát tokenu | Datový nosič |

---

# OAuth 2.0
- https://oauth.net/2/
- **Delegovaná autorizace** – aplikace získá omezený přístup ke zdrojům jménem uživatele
	- „Přihlásit přes Google" – Google vydá token, aplikace ho použije
- Uživatel nikdy nesděluje heslo třetí aplikaci
- Definuje **role**:
	- **Resource Owner** – uživatel vlastnící data
	- **Client** – aplikace žádající o přístup
	- **Authorization Server** – vydává tokeny
	- **Resource Server** – API chráněné tokeny

---

# OAuth 2.0 – typy tokenů
- **Access Token** – krátkodobý, opravňuje k přístupu na Resource Server
- **Refresh Token** – dlouhodobý, slouží k získání nového Access Tokenu bez přihlášení
- **Authorization Code** – dočasný kód vyměněný za tokeny (přenášen přes prohlížeč)
- Doporučený formát: **JWT** (ale OAuth 2.0 formát nestandardizuje)

---

# OAuth 2.0 – Authorization Code Flow

<pre style="font-size: 80%; line-height: 1.5">
Uživatel            Klient              Auth Server        Resource Server
   |                   |                    |                    |
   |–– přihlásit se ––>|                    |                    |
   |                   |–– redirect –––––––>|                    |
   |<––––––– login page ––––––––––––––––––– |                    |
   |–––––––– přihlásí se + souhlas ––––––––>|                    |
   |<––––––– redirect + auth_code ––––––––––|                    |
   |                   |<–– auth_code ––––––|                    |
   |                   |–– code + secret ––>|                    |
   |                   |<–– access_token –––|                    |
   |                   |–– access_token ––––––––––––––––––––––––>|
   |                   |<–– data ––––––––––––––––––––––––––––––––|
</pre>

<!-- .element: class="small" -->

---

# OAuth 2.0 – Grant typy
- **Authorization Code** – pro webové a mobilní aplikace (nejbezpečnější)
	- S rozšířením **PKCE** (Proof Key for Code Exchange) pro veřejné klienty
- **Client Credentials** – pro komunikaci server-server bez uživatele
- **Device Code** – pro zařízení bez prohlížeče (SmartTV, IoT)
- ~~Implicit~~ – zastaralý, nahrazen Authorization Code + PKCE
- ~~Resource Owner Password~~ – zastaralý, heslo putuje ke klientovi

---

# OAuth 2.0 – Scopes
- Rozsah oprávnění, o která aplikace žádá
- Definuje Resource Server, uživatel musí souhlasit
- Příklady (Google):
	- `openid` – základní identita
	- `email` – přístup k e-mailové adrese
	- `https://www.googleapis.com/auth/calendar` – kalendář
- Princip nejmenšího oprávnění – žádáme jen co potřebujeme

---

# OpenID Connect (OIDC)
- https://openid.net/connect/
- **Tenká autentizační vrstva nad OAuth 2.0**
	- OAuth 2.0 řeší autorizaci, OIDC přidává **autentizaci**
	- Klient se dozví *kdo* je uživatel, ne jen že má přístup
        - Např. jméno, e-mail, fotka
- Přidává:
	- **ID Token** – JWT s informacemi o uživateli (identity claims)
	- **UserInfo Endpoint** – dotaz na další claims
	- Standardizované claims: `sub`, `name`, `email`, `picture`, ...
	- **Discovery Dokument** – popis IdP na `/.well-known/openid-configuration`

---

# OIDC – ID Token
- JWT vydaný Auth Serverem po úspěšném přihlášení
- Standardní claims:
	- `iss` – vydavatel (IdP URL)
	- `sub` – unikátní identifikátor uživatele u IdP
	- `aud` – příjemce (Client ID aplikace)
	- `exp`, `iat` – expirace a čas vydání

```json
{
  "iss": "https://accounts.google.com",
  "sub": "110169484474386276334",
  "aud": "812741506391",
  "email": "jan.novak@gmail.com",
  "name": "Jan Novák",
  "exp": 1311281970
}
```
<!-- .element: class="small" -->

---

# OIDC – tok přihlášení

1. Klient přesměruje uživatele na IdP s parametry:
	- `response_type=code`, `scope=openid email`, `client_id`, `redirect_uri`, `nonce`
2. Uživatel se přihlásí u IdP
3. IdP přesměruje zpět s `code`
4. Klient vymění `code` za `access_token` + `id_token`
5. Klient ověří podpis a claims v `id_token`
6. Volitelně: dotaz na `userinfo` endpoint pro další data

---

# PKCE – Proof Key for Code Exchange
- Rozšíření Authorization Code Flow pro **veřejné klienty**
	- Mobilní aplikace, SPA (nemohou bezpečně uchovat client_secret)
- Princip:
	1. Klient vygeneruje náhodný `code_verifier`
	2. Odešle hash `code_challenge = SHA256(code_verifier)` s požadavkem
	3. Auth Server si uloží `code_challenge`
	4. Při výměně kódu klient pošle `code_verifier`
	5. Server ověří: `SHA256(code_verifier) == code_challenge`
- Chrání před zachycením `authorization_code`

---

# SAML 2.0
- https://www.oasis-open.org/committees/security/
- **Security Assertion Markup Language**
- Starší standard (2005), XML-based, rozšířený v podnicích
- Zaměřen na **SSO** mezi organizacemi (federace)
	- Např. přihlášení přes firemní IdP do externích SaaS aplikací
- Role:
	- **Identity Provider (IdP)** – spravuje uživatele, vydává assertions
	- **Service Provider (SP)** – aplikace, přijímá assertions

---

# SAML 2.0 – tok přihlášení (SP-initiated)

1. Uživatel přistoupí na SP (aplikaci)
2. SP přesměruje na IdP s `AuthnRequest`
3. Uživatel se přihlásí u IdP
4. IdP pošle **SAML Response** s podepsanou Assertion na SP (přes prohlížeč, POST)
5. SP ověří podpis a zpracuje assertions
6. Uživatel je přihlášen

- Assertion je podepsána privátním klíčem IdP, SP ověřuje veřejným klíčem

---

# Keycloak
- https://www.keycloak.org/
- Open-source **Identity and Access Management** server
- Implementuje OAuth 2.0, OIDC, SAML 2.0
- Správa uživatelů, rolí, skupin
- Federace s LDAP/Active Directory
- Sociální přihlášení (Google, GitHub, ...)
- Administrátorská konzole, REST API pro správu
- Alternativy: Auth0, Microsoft Entra ID, Okta, AWS Cognito

---

# OAuth2 / OIDC v Javě – MicroProfile JWT
- Ověření JWT access tokenů na straně Resource Serveru
- Neřeší samotný tok OAuth2 (přihlášení, výměna tokenů)
- Konfigurace ověření tokenu:

```properties
mp.jwt.verify.publickey.location=http://keycloak:8080/realms/myrealm/protocol/openid-connect/certs
mp.jwt.verify.issuer=http://keycloak:8080/realms/myrealm
mp.jwt.verify.audiences=my-client-id
```

- Roles z JWT claim `groups` nebo `realm_access.roles` (záleží na mapování)

---

# OAuth2 / OIDC v Javě – Jakarta Security 3.0
- Standard Jakarta EE 10
- `@OpenIdAuthenticationMechanismDefinition` – konfigurace OIDC klienta

```java
@OpenIdAuthenticationMechanismDefinition(
    providerURI = "http://keycloak:8080/realms/myrealm",
    clientId = "my-app",
    clientSecret = "${oidcConfig.clientSecret}",
    redirectURI = "${baseURL}/callback",
    jwksConnectTimeout = 5000
)
@ApplicationScoped
public class AppConfig { }
```

- Zvládá celý Authorization Code Flow automaticky
- Dostupné na Payara 6+, WildFly 27+

---

# Správa identit v Open Liberty
- Open Liberty podporuje všechny hlavní standardy přes **features**

| Feature | Účel |
|---------|------|
| `openidConnectClient-1.0` | OIDC klient (Relying Party) |
| `openidConnectServer-1.0` | OIDC provider (IdP) |
| `socialLogin-1.0` | OAuth2/OIDC sociální přihlášení |
| `samlWeb-2.0` | SAML 2.0 Web SSO |
| `mpJwt-2.1` | MicroProfile JWT (ověření tokenů) |
| `appSecurity-5.0` | Jakarta Security 3.0 (OIDC anotace) |

- Dokumentace: https://openliberty.io/docs/latest/single-sign-on.html

---

# Open Liberty – OIDC klient
- Feature `openidConnectClient-1.0` – Liberty jako OIDC Relying Party
- Konfigurace v `server.xml`, zvládá celý Authorization Code Flow

```xml
<featureManager>
    <feature>openidConnectClient-1.0</feature>
</featureManager>

<openidConnectClient
    id="myOIDC"
    clientId="my-app"
    clientSecret="secret"
    discoveryEndpointUrl=
      "http://keycloak:8080/realms/myrealm/.well-known/openid-configuration"
    redirectToRPHostAndPort="https://my-app.example.com"
    scope="openid profile email"
    userNameAttribute="preferred_username"
    groupIdentifier="groups" />
```
<!-- .element: class="small" -->

- Guide: https://openliberty.io/docs/latest/enable-openid-connect-client.html

---

# Open Liberty – SAML
- Feature `samlWeb-2.0` – Liberty jako SAML Service Provider
- Konfigurace v `server.xml`:

```xml
<featureManager>
    <feature>samlWeb-2.0</feature>
</featureManager>

<samlWebSso20 id="defaultSP"
    signatureMethodAlgorithm="SHA256"
    allowCustomCacheKey="false">
    <pkixTrustEngine trustAnchor="samlTrustStore" />
</samlWebSso20>

<keyStore id="samlTrustStore"
    location="saml-truststore.jks"
    type="JKS"
    password="changeit" />
```
<!-- .element: class="small" -->

- Metadata SP dostupná na `/ibm/saml20/{id}/samlmetadata`

---

# Open Liberty – Social Login
- Feature `socialLogin-1.0` – přihlášení přes OAuth2/OIDC providery
- Vestavěná podpora: GitHub, Google, Facebook, LinkedIn, Twitter
- Vlastní OAuth2 nebo OIDC provider:

```xml
<featureManager>
    <feature>socialLogin-1.0</feature>
</featureManager>

<oidcLogin id="keycloak"
    clientId="my-app"
    clientSecret="secret"
    discoveryEndpoint=
      "http://keycloak:8080/realms/myrealm/.well-known/openid-configuration"
    userNameAttribute="preferred_username" />

<!-- nebo pro čistý OAuth2: -->
<oauth2Login id="myProvider"
    clientId="..." clientSecret="..."
    authorizationEndpoint="https://provider/oauth/authorize"
    tokenEndpoint="https://provider/oauth/token" />
```
<!-- .element: class="small" -->

---

# Open Liberty – Jakarta Security (OIDC)
- Feature `appSecurity-5.0` – Jakarta Security 3.0
- Konfigurace výhradně anotacemi, **bez změn v `server.xml`**

```xml
<featureManager>
    <feature>appSecurity-5.0</feature>
</featureManager>
```

- Guide + Keycloak: https://openliberty.io/blog/2024/07/31/keycloak-with-openliberty.html

---

# Open Liberty – MicroProfile JWT
- Feature `mpJwt-2.1` – ověření JWT Bearer tokenů na Resource Serveru
- Konfigurace v `server.xml` nebo `microprofile-config.properties`

- Přístup k tokenu v kódu:

```java
@Inject
JsonWebToken jwt;

String user  = jwt.getSubject();
Set<String> roles = jwt.getGroups();
```

- Guide: https://openliberty.io/guides/microprofile-jwt.html

---

# Přístup k identitě v Javě

```java
@Inject
private OpenIdContext openIdContext;

@GET
@Path("/profile")
@RolesAllowed("user")
public String getProfile() {
    String subject = openIdContext.getSubject();
    Optional<String> email = openIdContext.getClaims()
        .getStringClaim("email");
    return "Přihlášen: " + email.orElse(subject);
}
```

---

# Refresh Token – princip
- **Access Token** je záměrně krátkodobý (minuty) – omezuje škody při úniku
- **Refresh Token** je dlouhodobý (hodiny–dny) a slouží k obnovení Access Tokenu **bez opětovného přihlášení uživatele**
- Refresh Token je uložen bezpečně u klienta, **nikdy se neposílá na Resource Server**

---

# Refresh Token – flow

<pre style="font-size: 80%; line-height: 1.5">
Klient              Auth Server        Resource Server
  |                    |                    |
  |–– access_token ––––––––––––––––––––––––>|
  |<–– 401 Unauthorized ––––––––––––––––––– |   (token expiroval)
  |                    |                    |
  |–– refresh_token ––>|                    |
  |<–– nový access_token + (nový refresh_token)
  |                    |                    |
  |–– nový access_token –––––––––––––––––––>|
  |<–– data ––––––––––––––––––––––––––––––– |
</pre>

<!-- .element: class="small" -->

---

# Refresh Token – bezpečnost
- **Refresh Token Rotation** – každým použitím se refresh token vyměňuje za nový
	- Starý token je okamžitě invalidován
	- Detekce opětovného použití (_reuse detection_): pokud někdo použije starý token, celá rodina tokenů se revokuje
- **Revokace** – refresh token lze explicitně zneplatnit (odhlášení, změna hesla)
	- RFC 7009: Token Revocation Endpoint
- Refresh Token **neobsahuje** data uživatele – je to neprůhledný (opaque) identifikátor nebo JWT s minimálními claims

---

# Doporučené postupy
- Nikdy neukládejte tokeny do `localStorage` – použijte `HttpOnly` cookies nebo server-side session
- Vždy ověřujte podpis tokenu a claim `iss`, `aud`, `exp`
- Používejte krátkou expiraci Access Tokenu (minuty), delší Refresh Tokenu
- **PKCE** pro všechny veřejné klienty
- Minimalizujte scopes – žádejte jen nezbytné
- Rotujte Refresh Tokeny (_refresh token rotation_)
- HTTPS všude – tokeny jsou citlivé přihlašovací údaje
