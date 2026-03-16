<!-- .slide: class="section" -->

<header>
	<h1>Jazyk CSS</h1>
	<p>úvod, principy</p>
</header>

---

# CSS

- CSS = <i>Cascading Style Sheet</i>
- *standardní* jazyk pro tvorbu stylových předpisů
  - **[specifikaci](https://www.w3.org/Style/CSS/)** spravuje W3C (World Wide Web), čitelnější podoba: **[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS)**

<br>

- **počátky (1994 - 1996)** -- vznik CSS, první specifikace (*CSS1*), základní styly pro text a barvy
- **rozvoj (1998 - 2000)** -- *CSS2* přináší pozicování, vrstvy, media typy
  - ⚠️ nejednotná podpora v prohlížečích
- **modularizace a CSS3 (2001 - 2010)** -- vývoj rozdělen na ***moduly*** (*CSS 3*)
  - flexbox, animace, pokročilé selektory, responzivní media queries
- **moderní layouty (2011 - 2020)** -- větší důraz na responzivní design a mobilní web
  - 2011 -- [CSS 2.1 W3C Recommendation](https://www.w3.org/TR/2011/REC-CSS2-20110607/) -- ✅ stabilní, podporované prohlížeči
  - CSS Grid, custom properties (proměnné)
- **současnost (2021 - dnes)** -- container queries, subgrid, selektor :has(), nativní nesting a Houdini API
  - *CSS 3+* moduly

---

# Stylový předpis

- ***<i>style sheet</i>*** = stylový předpis

- ***posloupnost pravidel*** týkající se různých *elementů* určující jejich ***vlastnosti*** 
  - např. barva a tloušťka fontu elementů `<p>`
  - typicky více pravidel pro každý element

<br>

- zdroje stylových předpisů:
   1. *styl připravený tvůrcem stránek*
   2. uživatelský styl (<i>user stylesheets</i>) - vlastní definice uživatele
   3. styl prohlížeče (<i>user agent styles</i>)

<br>

- relevantní pravidla se seřadí do ***kaskády***
  - kompletně definují výsledný vzhled (vlastnosti) každého elementu

---

# Připojení k HTML dokumentu

- ***externí***, ***interní*** a ***inline*** stylový předpis

```html
<head>
  <!-- externí stylový předpis -->
  <link rel="stylesheet" type="text/css" href="style.css"> 
  
  <!-- interní stylový předpis -->
  <style>
	/* Jazyk CSS uvnitř HTML dokumentu */
    p {
	  color: gray;
    }
  </style>
</head>

<body>
  <!-- inline stylový předpis -->	
  <p style="font-weight: bold; font-style: italic;"></p>
</body>
```

- ***pozor na priority!*** -- dále...

---

# Syntax CSS

```css
/* pravidlo */
selektor { 
	vlastnost: hodnota;
	vlastnost: hodnota;
	...
}

/* další pravidlo */
selektor {
	vlastnost: hodnota;
	vlastnost: hodnota;
	...
}

... 
```

- ***selektor*** -- určuje, pro které elementy dané pravidlo platí
- ***vlastnost*** -- definuje vizuální (případně další) charakteristiky dotyčných elementů