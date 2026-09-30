<!-- .slide: class="section" id="cookies" -->

<header>
    <h1>Příklad #2:<br>Cookies</h1>
</header>

---

# Cookies

- malý text uložený v prohlížeči -- server ho pošle hlavičkou `Set-Cookie`, prohlížeč ho vrací v hlavičce `Cookie` (jen na daný web a cestu)
- zpřístupněny ke čtení pomocí superglobálu [**$_COOKIE**](https://www.php.net/manual/en/reserved.variables.cookies.php)
	- nová hodnota v něm bude až při dalším požadavku
- zapisují se pomocí [**setcookie()**](https://www.php.net/manual/en/function.setcookie.php) -- volat před výstupem (je to [HTTP hlavička](#/hlavicky))

```php
setcookie("jazyk", // jméno
   "cs",           // hodnota
   time()+3600,    // expirace za hodinu (Unix timestamp)
   "/");           // cesta
```
<!-- .element: class="small" -->

- bez expirace obvykle do zavření prohlížeče, smazání = expirace v minulosti, [další parametry](https://www.php.net/manual/en/function.setcookie.php)
---

# Příklad práce s cookies

```php [2,4]
<?php
$pocet = (int) ($_COOKIE['pocet'] ?? 0); // od klienta → číslo
$pocet++;
setcookie('pocet', $pocet);
if($pocet == 1): // poprvé ?>
   <h1> Vítáme Vás poprvé na našem serveru.</h1>
<?php else: // není to poprvé ?>
   <h1> Jde o Váš <?= $pocet ?> přístup
   na tuto stránku.</h1>
<?php endif; ?>
```

<p class="small"><a href="https://www.fit.vut.cz/study/course/IIS/private/examples/cookies.php">příklad…</a></p>

---

<!-- .slide: id="bezpecne-cookies" -->

# Bezpečné cookies

- Od PHP 7.3 lze parametry předat polem

```php
setcookie('jazyk', 'cs', [
   'expires'  => time() + 3600,
   'path'     => '/',
   'secure'   => true,   // jen přes HTTPS
   'httponly' => true,   // nedostupné z JavaScriptu (omezí krádež přes XSS)
   'samesite' => 'Lax',  // cizí weby: jen GET navigace celé stránky (CSRF)
]);
```
<!-- .element: class="small" -->

- Cookie může uživatel přečíst i změnit -- nevkládat citlivá data (heslo, role) a hodnotám nevěřit
- Omezená velikost (cca 4 KB) -- data o přihlášeném uživateli patří do [session](#/session)
