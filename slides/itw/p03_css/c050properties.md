<!-- .slide: class="section" -->

<header>
	<h1>Vlastnosti</h1>
	<p>úvod, principy</p>
</header>

---

# Vlastnost

- určuje jak se vybrané elementy zobrazí (barva, rozměry, rozložení, písmo, animace atd.)
  - např. `color`, `font-size`, `margin`, `display`, ...
- množina vlastností je definována ve **[W3C CSS specifikaci](https://www.w3.org/Style/CSS/current-work)**

```css
color: blue;
font-size: 12pt;
```

- vlastnosti mají různé jednotky a formáty hodnot, někdy i experimentální varianty s prefixy
  - `-webkit-` Chrome, Safari (WebKit)
  - `-moz-` Firefox (Mozilla)
  - `-ms-` Internet Explorer, Edge (Trident/EdgeHTML)
  - `-o-` Opera (starý Presto engine)

---

# Typy vlastností

  - ***typografie a text*** -- ovlivňují písmo a textový obsah
    - `font-family`, `font-size`, `font-weight`, `color`, `text-align`, `line-height`, ...
  - ***barvy a pozadí*** -- řídí vzhled pozadí a barevné schéma
    - `background-color`, `background-image`, `background-position`, `opacity`, ...
  - ***box model (rozměry a okraje)*** - určují velikost, vnější a vnitřní odsazení, rámečky
    - `width`, `height`, `margin`, `padding`, `border`, `box-sizing`, ...
  - ***rozložení a pozicování (layout)*** -- ovlivňují, jak se elementy skládají a zarovnávají
    - `display`, `position`, `float`, `z-index`, ...
    - Flexbox
    - CSS Grid

---

# Typy vlastností

  - ***seznamy a tabulky*** -- vlastnosti pro speciální elementy
    - `list-style-type`, `list-style-image`, `border-collapse`, `caption-side`, ...
  - ***transformace, přechody a animace*** -- umožňují pohyb, efekty a interaktivitu.
    - `transform`, `transition`, `animation`, ...
  - ***filtry a efekty***
    - `filter`, `backdrop-filter`, `mask`, ...
  - ***interaktivita a kurzor***
    - `cursor`, `pointer-events`, `user-select`, ...
  - ***obsah a generované prvky*** -- přidávají nebo mění obsah vygenerovaný CSS.
    - `content`, `quotes`, `counter-reset`, `counter-increment`, ...

---

# Vlastnosti písma

- **styl písma -- *`font-style`***

<pre class="code-render" default-style="" resizable="true" style="height: 100px;">

<span style="font-style: normal">normal</span>
<span style="font-style: italic">italic</span>
<span style="font-style: oblique">oblique</span>

</pre>

- **váha písma -- *`font-weight`***

<pre class="code-render" default-style="" resizable="true" style="height: 100px;">

<span style="font-weight: normal">normal</span>
<span style="font-weight: lighter">lighter</span>
<span style="font-weight: bold">bold</span>
<span style="font-weight: bolder">bolder</span>
<span style="font-weight: 100">100</span>
<span style="font-weight: 900">900</span>

</pre>

- **varianta písma -- *`font-variant`***

<pre class="code-render" default-style="" resizable="true" style="height: 100px;">

<span style="font-variant: normal">normal</span>
<span style="font-variant: small-caps">small-caps</span>

</pre>

---

# Velikost písma

- ***`font-size`***

<pre class="code-render" default-style="
html {
  font-size: 16px;
}

body {
  transform: scale(2);
  transform-origin: 0 0;
  width: 49%;
}
" resizable="true" style="height: 300px;">

<span style="font-size: 16px">16px</span>
<span style="font-size: 32px">32px</span>
<span style="font-size: 1rem">1rem</span>
<span style="font-size: 2rem">2rem</span>
<span style="font-size: 100%">100%</span>
<span style="font-size: 200%">200%</span>
<br>
<br>
<span style="font-size: small">small</span>
<span style="font-size: x-small">x-small</span>
<span style="font-size: xx-small">xx-small</span>
<span style="font-size: medium">medium</span>
<span style="font-size: large">large</span>
<span style="font-size: x-large">x-large</span>
<span style="font-size: xx-large">xx-large</span>

</pre>

```css
html {
  /* nastavení velikosti 1rem */
  font-size: 16px;
}
```

---

# Druh písma

- ***`font-family`***

- generické druhy písem:

<pre class="code-render" default-style="
html {
  font-size: 32px;
}

body {
  transform: scale(2);
  transform-origin: 0 0;
  width: 49%;
}
" resizable="true" style="height: 130px;">

<span style="font-family: serif">serif</span>
<span style="font-family: sans-serif">sans-serif</span>
<span style="font-family: monotype">monotype</span>

</pre>

- nainstalovaná písma:

<pre class="code-render" default-style="
html {
  font-size: 32px;
}

body {
  transform: scale(2);
  transform-origin: 0 0;
  width: 49%;
}
" resizable="true" style="height: 300px; float: right; width: 35%; z-index: 1;">

<span style="font-family: Verdana Arial">Verdana</span><br>
<span style="font-family: 'Times New Roman'">Times New Roman</span>

</pre>

```css
span.verdana {
  font-family: Verdana, Arial, sans-serif;
}

span.times {
  font-family: "Times New Roman", sans-serif;
}
```

- je nutné vždy specifikovat ***alternativy*** (*poslední musí být generická*)
- pokud název obsahuje mezery, musí být v úvozovkách

---

# Externí fonty

- [Google Fonts](https://fonts.google.com/share?selection.family=Ubuntu)

- import CSS obsahující definici fontu v HTML:

```html
<head>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Ubuntu:ital,
    wght@0,300;0,400;0,500;0,700;1,300;1,400;1,500;1,700&display=swap" rel="stylesheet">
</head>

```

- použití fontu v CSS:

<pre class="code-render" default-style="
html {
  font-size: 64px;
}

body {
}
" resizable="true" style="height: 150px; float: right; width: 35%; z-index: 1;">

<span style="font-family: 'Ubuntu'">Ubuntu</span>

</pre>


```css
span.ubuntu {
  font-family: "Ubuntu", sans-serif;
  /* dle podpory fontu */
  font-weight: 400;
  font-style: normal;
}
```

---

# Vlastní font

- pravidlo ***@font-face*** umožňuje načíst vlastní font (např. z .woff2 nebo .ttf souboru) a používat ho v dokumentu

```css
@font-face { 
  font-family: 'NovyFont';
  src: url('newFontFile.woff') format('woff'),
       url('newFontFile.ttf') format('truetype'),
       url('newFontFile.svg') format('svg'); 
  font-weight: bold; 
  font-style: italic;
  font-stretch: normal; /* řez písma */
}


h1 {
  font-family: 'NovyFont', sans-serif;
  font-weight: bold;
  font-style: italic;
} 
```

---

# Vlastnosti textu

- **dekorace textu -- *`text-decoration`*** (`-style`, `-color`, `-thickness`)

<pre class="code-render" default-style="" resizable="true" style="height: 100px;">

<span style="text-decoration: none">none</span>
<span style="text-decoration: overline 2px">overline</span>
<span style="text-decoration: underline 2px">underline</span>
<span style="text-decoration: line-through 2px">line-through</span>
<span style="text-decoration: underline red 6px">underline red 6px</span>

</pre>

- **transformace textu -- *`text-transform`***

<pre class="code-render" default-style="" resizable="true" style="height: 100px;">

<span style="text-transform: none">none</span>
<span style="text-transform: capitalize">capitalize</span>
<span style="text-transform: uppercase">uppercase</span>
<span style="text-transform: lowercase">lowercase</span>

</pre>

- **mezera mezi písmeny -- *`letter-spacing`***

<pre class="code-render" default-style="" resizable="true" style="height: 100px;">

<span style="letter-spacing: normal">normal</span>&nbsp;&nbsp;&nbsp;&nbsp;
<span style="letter-spacing: .5rem">.5rem</span>

</pre>

- **mezera mezi slovy -- *`word-spacing`***

<pre class="code-render" default-style="" resizable="true" style="height: 100px;">

<span style="word-spacing: normal">normal word spacing</span>&nbsp;&nbsp;&nbsp;&nbsp;
<span style="word-spacing: .5rem">.5rem word spacing</span>

</pre>

---

# Zarovnání textu


- **horizontální zarovnání -- *`text-align`***
  - aplikuje se na blokový element, který obsahuje text (např. `<p>`)

<pre class="code-render" default-style="" resizable="true" style="height: 250px;">

<div style="text-align: left">left</div>
<div style="text-align: center">center</div>
<div style="text-align: right">right</div>
<div style="text-align: justify">justify</div>

</pre>

- **vertikální zarovnání -- *`vertical-align`***

<pre class="code-render" default-style="" resizable="true" style="height: 120px;">

<span style="vertical-align: baseline">baseline</span>
<span style="vertical-align: sub">sub</span>
<span style="vertical-align: super">super</span>
<span style="vertical-align: top">top</span>
<span style="vertical-align: bottom">bottom</span>
<span style="vertical-align: 30%">30%</span>

</pre>

---

# Mezery

<pre class="code-render" default-style="
p {
  text-align: justify;
  line-height: 1.8;       /* výška řádku */
  text-indent: 50px;      /* odsazení prvního řádku */
  overflow-wrap: break-word; /* zalomení dlouhých slov */
  word-break: break-word; /* láme při nutnosti */
  hyphens: auto;          /* dělení slov pomlčkami */
}" resizable="true" style="height: 800px; width: 30%; float: right; z-index: 1; margin-left: 1rem">

<p>
  Tento odstavec ukazuje, jak CSS vlastnosti pro rozvržení řádků fungují.
  Všimni si větší výšky řádků, odsazeného prvního řádku i toho, že dlouhá
  slova se v případě potřeby zalamují a mohou se rozdělit pomlčkou na konci.
  SlovoSuperExtraMegaUltraDlouhéSlovoBezMezer by jinak přetékalo ven z boxu.
</p>

</pre>

```css
p {
  text-align: justify;
  line-height: 2;       /* výška řádku */
  text-indent: 50px;      /* odsazení prvního řádku */
  overflow-wrap: break-word; /* zalomení dlouhých slov */
  word-break: break-word; /* láme při nutnosti */
  hyphens: auto;          /* dělení slov pomlčkami */
}
```

---

# Barva a stíny textu

- ***`color`***`: blue; `***`text-shadow`***`: offset-x offset-y blur-radius color;`

<pre class="code-render" default-style="
p {
  font-size: 2rem;
}

p.simple {
  text-shadow: 4px 4px 20px black; /* jednoduchý jemný stín */
}

p.multiple {
  text-shadow: 
    4px 4px 2px red,
    -4px -4px 2px blue; /* více stínů současně */
}

p.neon {
  color: #0f0;
  text-shadow:
    0 0 5px #0f0,
    0 0 10px #0f0,
    0 0 20px #0f0,
    0 0 40px #0f0; /* neonový efekt */
}" resizable="true" style="height: 600px; width: 50%; float: right; z-index: 1; margin-left: 1rem">

<p class="simple">Jednoduchý stín</p>
<p class="multiple">Vícebarevné stíny</p>
<p class="neon">Neonový text</p>

</pre>

```css
p.simple {
  text-shadow: 4px 4px 10px black;
}

p.multiple {
  text-shadow: 
    4px 4px 2px red,
    -4px -4px 2px blue;
}

p.neon {
  color: #0f0;
  text-shadow:
    0 0 5px #0f0,
    0 0 10px #0f0,
    0 0 20px #0f0,
    0 0 40px #0f0;
}
```

---

# Pozadí: barva, obrázek, opakování

- ***`background-color`***`: teal; `***`background-image`***`: url(...);`
- ***`background-repeat`***`: repeat | repeat-x | repeat-y | no-repeat;`

<pre class="code-render" default-style="
body {
      font-family: sans-serif;
      display: flex;
      flex-wrap: wrap;
      gap: 20px;
      padding: 20px;
      background: #f0f0f0;
    }

    div {
      color: blue;
      width: 400px;
      height: 300px;
    }

    /* Jednotlivé příklady */
    .color {
      background-color: teal;
    }

    .image {
      background-image: url('https://www.fit.vut.cz/study/course/ITW/public/assets/cat-fall-small.jpg');
    }

    .repeat {
      background-image: url('https://www.fit.vut.cz/study/course/ITW/public/assets/cat-fall-small.jpg');
      width: 100%;
      background-repeat: repeat-x;
    }
" resizable="true" style="height: 700px; width: 50%; float: right; z-index: 1; margin-left: 1rem">

  <div class="color">background-color</div>
  <div class="image">background-image</div>
  <div class="repeat">background-repeat</div>

</pre>

```css
.color {
  background-color: teal;
}

.background {
  background-image: url("cat.jpg");
}

.repeat {
  background-image: url("cat.jpg");
  background-repeat: repeat-x;
}
```

- deafult hodnota *`background-repeat`* je ***`repeat`***

---

# Pozadí: velikost, pozice, kombinace pozadí

- ***`background-size`***`: auto | 200px | 50% 200px | cover | contain | ...;`
- ***`background-position`***`: 10px 20px | 50% 50% | top left | ...;`

<pre class="code-render" default-style="
.box {
  width: 100%;
  height: 600px;

  /* Více vrstev pozadí */
  background-image: 
    url('https://www.fit.vut.cz/study/course/ITW/public/assets/gandalf.png'),
    url('https://www.fit.vut.cz/study/course/ITW/public/assets/cat-fall-small.jpg');

  background-repeat: no-repeat, no-repeat;
  background-size: 200px, cover;
  background-position: top left, center;
}
" resizable="true" style="height: 700px; width: 50%; float: right; z-index: 1; margin-left: 1rem">

  <div class="box"></div>

</pre>

```css
.box {
  width: 100%;
  height: 600px;

  background-image:
    url('gandalf.jpg'),
    url('cat.jpg');

  background-repeat:
    no-repeat,
    no-repeat;
  background-size:
    200px,
    cover;
  background-position:
    top left,
    center;
}
```

---

# Rámečky a stíny boxu

<pre class="code-render" default-style="
.box {
  box-sizing: border-box;
  width: 90%;
  height: 600px;
  margin: auto;
  margin-top: 50px;
  border-radius: 40px 20% 80px 10%;
  border: 10px solid red;
  box-shadow: inset 0px 0px 50px 5px yellow,
              0px 0px 50px 5px red;

  /* Více vrstev pozadí */
  background-image: 
    url('https://www.fit.vut.cz/study/course/ITW/public/assets/cat-fall-small.jpg');

  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
}
" resizable="true" style="height: 800px; width: 50%; float: right; z-index: 1; margin-left: 1rem">

  <div class="box"></div>

</pre>

```css
.box {
  border:
    10px solid red;
  border-radius:
    40px 20% 80px 10%;
  box-shadow:
    inset 0px 0px 50px yellow,
    0px 0px 50px red;
}
```

- ***`border`***`: thickness style color`
- ***`border-radius`***`:`
   - `20px;`
   - `TL TR BR BL;`
- ***`box-shadow`***`: offset-x offset-y blur-radius spread-radius color inset`  

---

# Zobrazení

- ***`display`***`:`
  - `none` -- prvek se vůbec nezobrazí (nezabírá místo)
  - `block` -- blokový prvek (zabírá celou šířku, začíná na novém řádku)
  - `inline` -- řádkový prvek (tekoucí v řádku, neumožňuje měnit šířku/výšku)
  - `inline-block` -- řádkový, ale s možností nastavit šířku/výšku

<br>


- ***pozicování a tvorba layoutů...***
  - `table`, `inline-table`
  - `table-row`, `table-cell`, ...
  - `flex`
  - `grid`