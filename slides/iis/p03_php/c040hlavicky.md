<!-- .slide: class="section" id="hlavicky" -->

<header>
    <h1>Příklad #1:<br>HTTP hlavičky</h1>
</header>

---

# HTTP hlavičky

- většinu hlaviček generuje HTTP server automaticky
- funkce [**header()**](https://www.php.net/manual/en/function.header.php)
	- `header('Content-type: image/png');`
- hlavičky je možno přidávat jen dokud nebyl zahájen přenos obsahu
	- přenos se zahájí prvním výstupem (např. **echo**)
	- nebo i část dokumentu mimo `<?php ?>` (!)
- funkce [**headers_sent()**](https://www.php.net/manual/en/function.headers-sent.php)
	- vrací true, pokud už byly hlavičky poslány (již nelze definovat další)

---

# Nejpoužívanější HTTP hlavičky

- **Content-Type** -- MIME typ obsahu (nejčastěji text/html), např.
	- `Content-Type: text/html; charset=utf-8`
	- `Content-Type: image/jpeg`
	- `Content-Type: application/json` (data pro JavaScript, REST API)
- **Location** -- přesměrování na jinou stránku, např.
	- `Location: https://www.jinde.cz/nove/`
- další: **Set-Cookie** (viz [Cookies](#/cookies)), **Cache-Control** (ukládání do cache), **Content-Disposition** (stažení souboru)

---

# Příklad přesměrování

```php [3,8,12]
function redirect_to($dest)
{
   if (headers_sent()) {
      ?>
      větev klienta
      <br>
      <script type="text/javascript">
         location.href = "<?php echo $dest;?>";
      </script>
      nedošlo k přesměrování v javascriptu
      <br>
      <a href="<?=$dest;?>">pokračovat</a>
      <?php
   } // if headers
```
<!-- .element: class="small" style="width:62%;margin-left:0" -->

<p class="small" style="margin-top:0">Pozor: pokud <code>$dest</code> pochází od uživatele, hrozí <em>open redirect</em> a XSS -- hodnotu ověřit a escapovat podle kontextu (HTML: <code>htmlspecialchars()</code>, JavaScript: <code>json_encode()</code>)</p>

<div class="cite" style="position:absolute;left:1240px;top:200px;width:560px;text-align:center;background:#fff">
Pokud byly hlavičky odeslány, nelze přesměrovat v PHP, ale až na klientovi<br>
(využití klientského JavaScriptu, případně HTML značky <em>meta refresh</em>)
</div>

---

# Příklad přesměrování

```php [11]
   else {
      $script = $_SERVER["SCRIPT_NAME"];
      if (strpos($dest, '/') === 0) { // absolute path
         $path = $dest;
      } else {
         $path = substr($script, 0,
                        strrpos($script, "/"))."/$dest";
      }
      $https = $_SERVER["HTTPS"] ?? "";
      $scheme = ($https && $https !== "off") ? "https" : "http";
      header("Location: $scheme://{$_SERVER['HTTP_HOST']}$path");
      exit();
   } // else
} // of redirect_to
```
<!-- .element: class="small" style="width:71%;margin-left:0" -->

<div class="cite" style="position:absolute;left:1350px;top:500px;width:460px;text-align:center;background:#fff">
Jinak můžeme přesměrovat pomocí funkce header().<br>
Složíme jméno pro přesměrování s využitím <strong>$_SERVER</strong>.
</div>

---

# Přesměrování dnes

- Hlavička `Location` může obsahovat i relativní adresu ([RFC 9110](https://www.rfc-editor.org/rfc/rfc9110.html#name-location)) -- celou URL z `$_SERVER` není nutné skládat

```php
header('Location: vysledek.php');   // relativně k URL požadavku
header('Location: /admin.php');     // od kořene serveru
exit;                               // po přesměrování ukončit skript
```

- Výchozí stavový kód je **302 Found**
- Po zpracování formuláře (POST) je vhodnější **303 See Other**
	- prohlížeč načte cílovou stránku metodou GET a obnovení stránky (F5) neodešle formulář znovu -- vzor *Post/Redirect/Get*

```php
header('Location: vysledek.php', true, 303);
```

---

# Stavové kódy a výstupní buffer

- [**http_response_code()**](https://www.php.net/manual/en/function.http-response-code.php) -- nastaví [stavový kód](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status) odpovědi (200 OK, 403 Forbidden, 404 Not Found, …)

```php
if (!$produkt) {
   http_response_code(404);
   echo "Produkt nenalezen";
   exit;
}
```
<!-- .element: class="small" -->

- **Výstupní buffer** -- výstup se ukládá do paměti a odešle se až později, hlavičky lze proto nastavit i po `echo`
	- [**ob_start()**](https://www.php.net/manual/en/function.ob-start.php) ve skriptu, nebo `output_buffering` v `php.ini` (často zapnuto, např. 4096 B)
	- proto `header()` po `echo` někdy „funguje“ -- nespoléhat na to
