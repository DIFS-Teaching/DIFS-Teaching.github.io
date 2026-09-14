<!-- .slide: class="section" -->

<header>
	<h1>Smím to vůbec?</h1>
	<p>Technicky vás nic nezastaví. To ale není totéž jako svolení.</p>
</header>

---

# robots.txt

- Dohoda, ne zámek &ndash; **je to prosba, ne technická překážka**
- Web tu říká, co si přeje, aby roboti nestahovali

```
# www.fit.vut.cz/robots.txt
User-agent: *
Disallow: /search/
Request-rate: 5/1s

User-agent: GPTBot
Disallow: /
```
<!-- .element: class="col" -->

```
# www.sreality.cz/robots.txt
User-agent: *
Disallow: /

#    neplecha ukončena

User-agent: Googlebot
Allow: /
```
<!-- .element: class="col" -->

- ??**Rozlišuje, kdo jste, ne co děláte** &ndash; Googlebot smí, vy ne
- ??Opačná strana téže mince: `sitemap.xml` vám sám řekne, co stáhnout

Note:
Komentář &bdquo;neplecha ukončena&ldquo; v robots.txt Srealit je autentický.
Dobrá ilustrace toho, že za tím souborem sedí člověk, kterého něco naštvalo.

FIT si přes `Request-rate` říká o nejvýš pět požadavků za sekundu
a blokuje GPTBot &ndash; k tomu se vrátíme na dalším slajdu, není to náhoda.

---

# Co smím a co ne

<p class="cite" style="font-size: 85%">
Use of any device, tool, or process designed to data mine or scrape the content
using automated means is prohibited without prior written permission from IMDb.
<br><em>&ndash; imdb.com/robots.txt, a tahle přednáška IMDb používá jako příklad</em>
</p>

<div class="small">

- **Podmínky užití** jsou smlouva; `robots.txt` je konvence, ne zákon
- **Autorské právo** k obsahu &ndash; texty, fotografie, popisy produktů
- **Zvláštní právo pořizovatele databáze** &ndash; chrání i obsah, který sám autorský není
- ??**Výjimka pro vytěžování textů a dat** (TDM), směrnice 2019/790:
	- `§ 39c` &ndash; obecná, ale nositel práv si ji může **strojově čitelně vyhradit**
	- `§ 39d` &ndash; pro vědecký výzkum na VŠ, tuhle vyloučit nelze
- **Osobní údaje** &ndash; GDPR platí i na údaje veřejně dostupné

</div>

- ??Kde se ta výhrada podle `§ 39c` dělá? ||**V robots.txt.**||
- ??**Veřejně dostupné &ne; volně použitelné**

Note:
Nejsem právník a tenhle slajd není právní rada, je to orientace v tom,
čeho se vůbec ptát.

Pointa, kvůli které tu ty dva paragrafy jsou: soubor z minulého slajdu není
jen etiketa. Od novely z roku 2022 je to místo, kde se právně účinně vyhrazuje
strojové vytěžování. Blokace GPTBot na webu FIT je přesně tohle.

Pro školní projekt je situace mírnější než pro komerční využití, ale
&bdquo;bylo to na internetu&ldquo; obhajoba není.

---

# Slušný scraper

- **Představte se** &ndash; vlastní `User-Agent` včetně kontaktu na sebe
- **Choďte pomalu** &ndash; limit požadavků, exponenciální backoff
	- Respektujte `429 Too Many Requests` a hlavičku `Retry-After`
- **Nestahujte totéž dvakrát** &ndash; cache, podmíněné požadavky (`If-Modified-Since`)
- **Berte jen to, co potřebujete** &ndash; ne celý web kvůli jedné tabulce
- **Paralelizujte napříč doménami**, ne uvnitř jedné
- ??Malý web nemá vaši kapacitu &ndash; jde ho scraperem položit úplnou náhodou

<p class="fragment">
Anti-bot obrana (Cloudflare, CAPTCHA, fingerprinting) je srozumitelný vzkaz:
<strong>tady vás nechceme</strong>. Její obcházení je technicky i právně jiná liga.
</p>
