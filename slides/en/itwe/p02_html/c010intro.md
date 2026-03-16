<!-- .slide: class="quote" -->

# Motivation

> To present the ***content*** of a document,\
describe its ***structure***,\
and the ***meaning*** of its individual parts.

=--

<!-- .slide: class="editor" -->

# Motivation -- Example

<div data-iframe="assets/examples/tyrion/tyrion.html"></div>

<div class="note"><a href="assets/examples/tyrion.html">source</a></div>

---

# Markup Languages

- A tool for creating documents, defining structure and meaning

<br>

- **Traditional programming languages** -- dominated by *structured text* (source code), general text appears as ***<i>strings</i>***

<img src="assets/html-programmer.jpg" alt="HTML programmer" class="img-right box">

```c
if(strcmp("I am not in danger, Skyler.", msg) == 0)
  printf("I am the danger.");
```

<br>

- **Markup languages** -- dominated by *general text*, with structured sections inserted using ***<i>tags</i>***.

```html
You got one part of that wrong,
  <a href="mercury.html">this</a>
  is not <a href="crystal.html">meth</a>
```

<span class="note"><a href="https://www.youtube.com/watch?v=zAjJYkUnTEs">.</a></span>
<span class="note"><a href="https://www.youtube.com/watch?v=uBsR5y5uWjE">.</a></span>

---

# Types of Markup Languages

  - different in syntax and usage

<br>

  - **Data serialization, configuration** -- ***XML***, ***JSON***, YAML, TOML, INI, ...
  - **Printed documents**
    - TeX (LaTeX) -- publishing
    - Rich Text Format (RTF) -- office documents
  - **Electronic manuals** -- nroff, troff
  - **Electronic documents**
    - ***Markdown***, Wiki (DokuWiki, MediaWiki), ... -- using intuitive symbols
  - **Web pages**
    - XML family (***XHTML***, ***SVG***, MathML, ...)
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

<span class="note"><a href="https://www.markdownguide.org/basic-syntax/">documentation</a>,<span>
<span class="note"><a href="https://en.wikipedia.org/wiki/Markdown#Examples">comparison</a><span>

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

<span class="note"><a href="https://www.dokuwiki.org/wiki:syntax">documentation</a></span>

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