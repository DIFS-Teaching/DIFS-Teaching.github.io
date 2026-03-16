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
	- *Adresáře s právem zápisu*
	- `/var/*`, `/temp`, `/log` apod.

---

# Spolupráce s HTTP serverem Apache

- Apache musí mít přístup jen do adresáře s webovými soubory! 
- Konfigurace v souboru `.htaccess`
- Nejčastěji přepisování URL pomocí `mod_rewrite`
	- Přesměrování na front controller `index.php`
	- Ošetření výjimek
- Nastavení viditelnosti adresářů apod.

---

# Laravel

- Instalace a první aplikace \
	https://laravel.com/docs/8.x/installation
- Vlastní nástroj `laravel` nebo `composer`
- Demo aplikace
	- Jednoduchá https://github.com/laravel/quickstart-basic
	- RealWorld https://github.com/gothinkster/laravel-realworld-example-app/tree/master/app

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
	https://doc.nette.org/cs/3.0/quickstart/getting-started
- Používá `composer`
- Demo aplikace
	- https://github.com/nette/tutorial-quickstart/tree/v3.0

