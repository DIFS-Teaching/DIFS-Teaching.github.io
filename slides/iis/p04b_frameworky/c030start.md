<!-- .slide: class="section" -->

<header>
	<h1>Jak začít?</h1>
	<p>Instalace a první aplikace</p>
</header>

---
# Composer

- Většina frameworků používá [Composer](https://getcomposer.org/)
	- Vytvoření a správa projektu
	- Instalace závislostí
- Konfigurace projektu v souboru `composer.json`

---

# Struktura projektu

- Aplikace (`/app`, `/src`, apod.)
	- Implementace modelů, kontrolerů, ... (PHP stuff)
- Webové soubory (`/www`, `/public`)
	- Obsah přístupný serveru (statický)
	- `index.php`
	- `.htaccess`
- Konfigurační soubory aplikace
- Dočasné soubory
	- Adresáře s právem zápisu
	- `/var/*`, `/temp`, `/log` apod.

---

# Spolupráce s HTTP serverem

- Document root musí směřovat do `/www` či `/public`; ostatní soubory nesmějí být přímo dostupné přes HTTP!
- Apache
	- Konfigurace v souboru `.htaccess`
	- Nejčastěji přepisování URL pomocí `mod_rewrite`
		- Přesměrování na front controller `index.php`
		- Ošetření výjimek
	- Nastavení viditelnosti adresářů apod.
- nginx
	- Nepoužívá `.htaccess`, vše v konfiguraci serveru (`try_files`)
	- PHP spouští přes PHP-FPM (FastCGI)

---

# Laravel

- Instalace a první aplikace \
	https://laravel.com/docs/installation
- Vlastní nástroj `laravel` nebo `composer`
- Demo aplikace
	- Oficiální kurz https://laravel.com/learn/getting-started-with-laravel
	- Starter kity https://laravel.com/starter-kits

---

# Symfony

- Instalace a první aplikace \
	https://symfony.com/doc/current/setup.html
- Vlastní nástroj `symfony` nebo `composer`
- Demo aplikace
	- https://github.com/symfony/demo

---

# Nette

- Instalace a první aplikace \
	https://doc.nette.org/cs/quickstart
- Používá `composer`
- Demo aplikace
	- https://github.com/nette-examples/quickstart

