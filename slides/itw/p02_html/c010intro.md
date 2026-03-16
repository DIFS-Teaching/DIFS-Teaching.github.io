<!-- .slide: class="quote" -->

# Motivace

> Prezentovat ***obsah*** dokumentu\
a popsat jeho ***strukturu***\
a ***význam*** jeho jednotlivých částí.

=--

<!-- .slide: class="editor" -->

# Motivace -- příklad

<div data-iframe="assets/examples/tyrion/tyrion.html"></div>

<div class="note"><a href="assets/examples/tyrion.html">zdroj</a></div>

---

# Značkovací jazyky

- prostředek pro tvorbu dokumentů, definici struktury a významu

<br>

- **Klasické programovací jazyky** -- převládá *strukturovaný text* (programový kód), obecný text se vyskytuje ve formě ***<i>řetězců</i>***

<img src="assets/html-programmer.jpg" alt="HTML programmer" class="img-right box">

```c
if(strcmp("I am not in danger, Skyler.", msg) == 0)
  printf("I am the danger.");
```

<br>

- **Značkovací jazyky** -- převládá *obecný text*, do kterého vloženy strukturované úseky pomocí ***<i>značek</i>***. 

```html
You got one part of that wrong,
  <a href="mercury.html">this</a>
  is not <a href="crystal.html">meth</a>
```

<span class="note"><a href="https://www.youtube.com/watch?v=zAjJYkUnTEs">.</a></span>
<span class="note"><a href="https://www.youtube.com/watch?v=uBsR5y5uWjE">.</a></span>

---

# Typy značkovacích jazyků

  - liší se syntaxí a způsobem využití

<br>

  - **Serializace dat, konfigurace** -- ***XML***, ***JSON***, YAML, TOML, INI, ...
  - **Tištěné dokumenty**
    - TeX (LaTeX) -- publikace
    - Rich Text Format (RTF) -- kancelářské dokumenty
  - **Elektronické manuály** -- nroff, troff
  - **Elektronické dokumenty**
    - ***Markdown***, Wiki (DokuWiki, MediaWiki), ... -- intuitivní značkování pomocí symbolů
  - **Webové stránky**
    - Rodina XML (***XHTML***, ***SVG***, MathML, ...)
    - ***HTML***

=--

# Markdown

```md
# 🧙‍♂️ Severus Snape
> *“Always.”*

## Profile
- **Full Name:** Severus Tobias Snape  
- **House:** Slytherin  
- **Blood Status:** Half-blood  

## Roles & Affiliations
- Potions Master, Headmaster of Hogwarts  
- Member of the Order of the Phoenix  
- Former Death Eater

## Skills
- Expert in Potions and Dark Arts  
- Skilled in Occlumency & Legilimency  
- Inventor of spells (*e.g. Sectumsempra*)

## Portrayed By
Alan Rickman (2001–2011)
```

<span class="note"><a href="https://www.markdownguide.org/basic-syntax/">dokumentace</a>,<span>
<span class="note"><a href="https://en.wikipedia.org/wiki/Markdown#Examples">srovnání</a><span>

=--

# DokuWiki

```
====== 🧙‍♂️ Severus Snape ======
> ''"Always."''

===== Profile =====
  * **Full Name:** Severus Tobias Snape
  * **House:** Slytherin
  * **Blood Status:** Half-blood

===== Roles & Affiliations =====
  * Potions Master, Headmaster of Hogwarts
  * Member of the Order of the Phoenix
  * Former Death Eater

===== Skills =====
  * Expert in Potions and Dark Arts
  * Skilled in Occlumency & Legilimency
  * Inventor of spells (e.g. //Sectumsempra//)

===== Portrayed By =====
Alan Rickman (2001–2011)
```

<span class="note"><a href="https://www.dokuwiki.org/wiki:syntax">dokumentace</a></span>

=--

<!-- .slide: class="editor" -->

# HTML

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Severus Snape Profile</title>
</head>
<body>
  <h1>🧙‍♂️ Severus Snape</h1>
  <blockquote><em>"Always."</em></blockquote>

  <h2>Profile</h2>
  <ul>
    <li><strong>Full Name:</strong> Severus Tobias Snape</li>
    <li><strong>House:</strong> Slytherin</li>
    <li><strong>Blood Status:</strong> Half-blood</li>
  </ul>

  <h2>Roles & Affiliations</h2>
  <ul>
    <li>Potions Master, Headmaster of Hogwarts</li>
    <li>Member of the Order of the Phoenix</li>
    <li>Former Death Eater</li>
  </ul>

  <h2>Skills</h2>
  <ul>
    <li>Expert in Potions and Dark Arts</li>
    <li>Skilled in Occlumency & Legilimency</li>
    <li>Inventor of spells (e.g. <em>Sectumsempra</em>)</li>
  </ul>

  <h2>Portrayed By</h2>
  <p>Alan Rickman (2001–2011)</p>
</body>
</html>
```