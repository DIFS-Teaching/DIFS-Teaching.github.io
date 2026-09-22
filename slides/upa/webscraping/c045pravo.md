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

- **Rozlišuje, kdo jste, ne co děláte** &ndash; Googlebot smí, vy ne

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
<br><em>&ndash; imdb.com/robots.txt</em>
</p>

<div class="small">

- **Podmínky užití** jsou smlouva; `robots.txt` je konvence, ne zákon
- **Autorské právo** k obsahu &ndash; texty, fotografie, popisy produktů
- **Osobní údaje** &ndash; GDPR platí i na údaje veřejně dostupné
- Směrnice EU 2019/790

</div>

- **Veřejně dostupné &ne; volně použitelné**

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

<p>
Anti-bot obrana (Cloudflare, CAPTCHA, fingerprinting) je jasný vzkaz:
<strong>tady vás nechceme</strong>. Její obcházení je technicky i právně jiná liga.
</p>
