<!-- .slide: class="section" -->

<header>
	<h1>Automatizace prohlížeče</h1>
	<p>Když se ke stránce nedá dostat na jeden HTTP GET.</p>
</header>

---

# Mechanical Soup

- Automatizace ``prohlížeče'' pro [BeautifulSoup](#/beautifulsoup)
	- [Stránky projektu](https://github.com/MechanicalSoup/MechanicalSoup)
- Třídy a metody simulující základní operace HTTP
	- ``Klikání na odkazy'' -- zjištění cíle a generování GET požadavku
	- ``Vyplnění formulářů'' -- zjištění `action` a `method`, vyplnění hodnot polí a vyslání příslušného požadavku.
- JavaScript není podporován

---

# Puppeteer

- Chrome browser dálkově ovládaný z node.js\
  https://github.com/puppeteer/puppeteer
- Lze řídit navigaci prohlížeče
	- Zadání URL, klikání na odkazy, vyplňování formulářů
	- [API dokumentace](https://github.com/puppeteer/puppeteer/blob/v5.3.1/docs/api.md)
- Vykonání JS kódu v prohlížeči (`page.evaluate()`)
	- Např. pro extrakci obsahu z DOM

---

# Playwright

- Novější alternativa k puppeteer (původní vývojový tým)\
  https://playwright.dev
- Velmi podobné API i funkčnost
- Podpora více prohlížečů
	- Chromium/Chrome, Firefox, WebKit
- Více vývojových platforem
	- Node.js, Java, Python, .NET
- Mírně lepší dokumentace, možnosti konfigurace, ...

---

# Puppeteer Pros & Cons
- \+ Možnost navigace <!-- .element: class="plus" -->
- \+ Pohodlná extrakce dat <!-- .element: class="plus" -->
	- DOM, CSS Selektory, [**XPath**](#/xpath), jakýkoliv JavaScript
- \- Časově i prostorově náročné řešení <!-- .element: class="minus" -->
	- Spouští se celý Chrome
- \- Náročné ošetření vnějších podmínek <!-- .element: class="minus" -->
	- Např. časové souběhy, regionální verze stránek, ...
- \- Obtíženější ladění <!-- .element: class="minus" -->
	- Část JS kódu běží v node.js, část v prohlížeči (různá prostředí)

