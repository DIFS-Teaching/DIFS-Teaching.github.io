<!-- .slide: class="section" -->

<header>
	<h1>Automatizace prohlížeče</h1>
	<p>Když se ke stránce nedá dostat na jeden HTTP GET.</p>
</header>

---

# Nejdřív levnější mezistupeň

- Spousta ``dynamických'' stránek celý prohlížeč nepotřebuje
- **HTTP relace** &ndash; `requests.Session()` nebo `httpx` v pythonu
	- Drží cookies, umí přesměrování i přihlášení formulářem
- [Mechanical Soup](https://github.com/MechanicalSoup/MechanicalSoup) &ndash; nadstavba nad [BeautifulSoup](#/beautifulsoup)
	- ``Klikání na odkazy'' &ndash; zjištění cíle a generování GET požadavku
	- ``Vyplnění formulářů'' &ndash; zjištění `action` a `method`, odeslání hodnot
- JavaScript ale nespustí ani jedno
	- ??Napřed se podívejte do **Network** v nástrojích prohlížeče &ndash; často se dá volat rovnou to API

---

# Playwright

- Prohlížeč dálkově ovládaný z kódu\
  https://playwright.dev
- Podpora více prohlížečů
	- Chromium/Chrome, Firefox, WebKit
- Více vývojových platforem
	- Node.js, Java, Python, .NET
- **Locator API s automatickým čekáním**
	- `page.locator("#list tr")` počká, až prvek existuje a je použitelný
	- Odpadá většina časových souběhů, kvůli kterým dřív scrapery náhodně selhávaly
- Vykonání JS kódu v prohlížeči (`page.evaluate()`)

---

# Playwright -- příklad

```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch()
    page = browser.new_page()
    page.goto("https://www.fit.vut.cz/study/courses/")

    for row in page.locator("#list tbody tr").all():
        cells = row.locator("td").all_inner_texts()
        print(";".join(c.strip() for c in cells))

    browser.close()
```

- ??`playwright codegen <adresa>` &ndash; naklikáte postup v prohlížeči a vypadne z toho kód
	- Nejrychlejší cesta od ``tohle potřebuju'' k funkčnímu scraperu

---

# Puppeteer

- Starší sourozenec, Chrome ovládaný z node.js\
  https://pptr.dev
- Velmi podobné API a možnosti
	- Ale jen Chrome/Chromium a jen JavaScript
	- Playwright založil původní vývojový tým Puppeteeru
- ??Pozor při čtení starších návodů
	- `page.$x()` pro XPath **už neexistuje**
	- Dnes se XPath píše jako selektor: `::-p-xpath(//h2)`

---

# Automatizace prohlížeče: Pros & Cons
- \+ Možnost navigace <!-- .element: class="plus" -->
- \+ Pohodlná extrakce dat <!-- .element: class="plus" -->
	- DOM, CSS selektory, [**XPath**](#/xpath), jakýkoliv JavaScript
- \+ Stránka se vidí tak, jak ji vidí uživatel <!-- .element: class="plus" -->
- \- Časově i prostorově náročné řešení <!-- .element: class="minus" -->
	- Spouští se celý prohlížeč &ndash; řádově pomalejší než jeden HTTP dotaz
- \- Náročné ošetření vnějších podmínek <!-- .element: class="minus" -->
	- Regionální verze stránek, cookie lišty, A/B testy
- \- Obtížnější ladění <!-- .element: class="minus" -->
	- Část kódu běží v node.js či pythonu, část v prohlížeči (různá prostředí)

---

# Crawling ve velkém

Vraťme se k prvnímu dílčímu problému: **jak vůbec ty dokumenty získat?**

- Fronta URL (*frontier*) a evidence už navštívených adres
- **Deduplikace** &ndash; tatáž stránka pod různými URL (`?utm_source=`, řazení, stránkování)
- Zdvořilostní prodleva mezi požadavky na tentýž server
- Cache a podmíněné požadavky, ať nestahujete totéž znovu
- Paralelizace **napříč doménami**, ne uvnitř jedné
- ??`sitemap.xml` &ndash; web vám sám nabídne seznam stránek
- ??Hotové rámce: [Scrapy](https://scrapy.org/) (Python), [Crawlee](https://crawlee.dev/) (Node.js, Python)
	- Frontu, opakování, rate limiting i export dat řeší za vás
