<!-- .slide: class="section" id="session" -->

<header>
    <h1>Příklad #4:<br>Session, autorizace</h1>
</header>

---

# Sessions v PHP

- data o uživateli jsou uložená **na serveru**, klient má v cookie jen náhodný identifikátor session (viz [Bezpečné cookies](#/bezpecne-cookies))
- identifikátor session se předává v cookie (výchozí název `PHPSESSID`) -- automaticky
- předávání identifikátoru v URL (konstanta `SID`, automatická úprava odkazů) je zastaralé
	- identifikátor uniká v historii, logách serveru a hlavičce `Referer`
	- od PHP 8.4 jeho zapnutí vyvolá varování *deprecated*

---

# Navázání sessions

- před jakýmkoli výstupem je třeba volat **session_start()** (posílá cookie v hlavičce)
- pokusí se načíst identifikátor `PHPSESSID`
	- z cookie
	- pokud žádný není přítomen, vytvoří nový identifikátor
- inicializuje související proměnné

---

# Předávání dat v session

- pole **$_SESSION** (superglobál)
- před použitím je nutno volat **session_start()**
- hodnoty zapsané do tohoto pole jsou dostupné během celé session

```php
$_SESSION["user"] = "root";
…
echo $_SESSION["user"];
```

---

# Příklad: autorizace

- chceme, aby některé části aplikace byly dostupné jen přihlášeným uživatelům (login a heslo)
	1. vytvoříme novou session
	2. požadujeme přihlašovací údaje
	3. pokud jsou v pořádku, uložíme do session identifikátor uživatele
	4. chráněné stránky ověří identifikátor uživatele v session
	5. odhlášení = vymazání identifikátoru ze session
- kroky 2--3 = **autentizace** (kdo uživatel je), krok 4 = **autorizace** (co smí)
- [příklad…](https://www.fit.vut.cz/study/course/IIS/private/examples/session/login.php), [demo (GitHub)](https://github.com/DIFS-Teaching/basic-demos/tree/master/php-session)

---

# Příklad: autorizace -- přihlašovací dialog (1)

```php [2,6,7]
<?php
session_start();
$login = $_POST['login'] ?? '';
$pwd = $_POST['pwd'] ?? '';
if($login == 'admin' && $pwd == 'SpravneHeslo') {
   session_regenerate_id(true); // nové ID po přihlášení
   $_SESSION['user'] = $login;
   header('Location: admin.php', true, 303);
   exit;
}
?>
```

---

# Příklad: autorizace -- přihlašovací dialog (2)

```php
<html>
<head></head>
<body>
   <form action="<?= htmlspecialchars($_SERVER['SCRIPT_NAME']) ?>"
         method="post">
   <label for="login">Login:</label>
   <input type="text" name="login" id="login"><br>
   <label for="pwd">Heslo:</label>
   <input type="password" name="pwd" id="pwd"><br>
   <input type="submit" value="Odeslat">
   </form>
</body>
</html>
```

---

# Příklad: autorizace -- autorizovaná stránka

```php [2,3,4]
<?php
   session_start();
   if(($_SESSION['user'] ?? '') !== 'admin') {
      header('Location: login.php');  // nepřihlášený → přihlášení
      exit();
   }
?>
<html>
   …
</html>
```

- přihlášený uživatel bez oprávnění → `http_response_code(403);` (Forbidden)

---

# Příklad: autorizace -- odhlášení

```php [2,3]
<?php
   session_start();
   unset($_SESSION['user']);
?>
<html>
   …
   Odhlášení proběhlo.
   …
</html>
```

- úplné zrušení celé session: `$_SESSION = []; session_destroy();` -- cookie s ID zůstane, smazat přes `setcookie()`
