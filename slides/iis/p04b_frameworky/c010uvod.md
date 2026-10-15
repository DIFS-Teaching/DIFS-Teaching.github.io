# Aplikační frameworky

- Rámcová řešení pro implementaci serverových aplikací
	- Neplést s klientskými frontend frameworky (v JavaScriptu)!
- Poskytují API (třídy a metody) pro běžné úlohy a situace
	- Zpracování požadavku apod.
- Vynucují pevnou strukturu aplikace
- Tvůrce se může soustředit na tvorbu vlastního řešení
	- Implementace aplikační logiky
	- Uživatelské rozhraní nebo API (volitelně)



---

<!-- .slide: class="normal centered" -->

# Vrstvy aplikace

![Vrstvy aplikace](assets/vrstvy.svg) <!-- .element: style="height: 750px; text-align: center" -->

---

# Nejdůležitější úlohy frameworku

- Zpracování HTTP požadavků
	- Dekódování požadavku a parametrů
	- Volání příslušné aplikační logiky
	- Generování odpovědi
- Tvorba GUI na serveru
	- Snadné generování výstupního HTML (šablony)
	- Znovupoužitelné komponenty (např. formuláře)
- Databázová vrstva
	- Jednotná komunikace s DB serverem
	- Jednotná konfigurace

---

# Další běžné funkce

- Jednotná konfigurace aplikace
- Správa instancí objektů a závislostí
	- Dependency injection
- Autentizace a autorizace

---

# Hlavní PHP frameworky

Populární v ČR:

- Laravel -- https://laravel.com/
- Symfony -- https://symfony.com/
- Nette -- https://nette.org/

Širší přehled:

- např. [Wikipedia: Comparison of server-side web frameworks](https://en.wikipedia.org/wiki/Comparison_of_server-side_web_frameworks#PHP)
- (ale podobných přehledů a žebříčků je mnoho)

---

<!-- .slide: class="normal centered" -->

# Je dobré použít framework?

??**ANO** <!-- .element: style="font-size:200%" -->

??(Pro produkční, déle udržovanou aplikaci)

- ??Přehledná struktura aplikace -- udržovatelnost, rozšiřitelnost
- ??Produktivita
- ??Bezpečnost (záleží na frameworku)

