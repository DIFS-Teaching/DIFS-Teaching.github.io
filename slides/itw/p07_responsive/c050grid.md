<!-- .slide: class="section" -->
 
<header>
    <h1>Grid systém: CSS Grid</h1>
</header>

---

# CSS Grid

- nástroj pro rozmísťování prvků ve dvou dimenzích (řádky + sloupce)
  - probráno v přednášce 6. CSS -- layouty
- zatím nejpokročilejší nástroj pro rozmísťování prvků v CSS
- umožňuje snadno definovat Grid systém bez zásahů do HTML dokumentu

<div class="img-right box" style="width: 700px; text-align: center;">
  <img src="assets/grid.svg" alt="CSS Grid" style="width: 100%;">
</div>

<br>

- layout se skládá z:
  1. ***kontejneru*** (<i>grid container</i>)
     - obsahuje *mřížku* (<i>grid</i>) složenou z *buněk* (<i>cells</i>)
     - skupiny buněk tvoří *oblastí* (<i>tracks</i>, <i>areas</i>),<br> na které jsou mapovány *položky kontejneru* (<i>grid items</i>)
  2. ***položek kontejneru*** (<i>grid items</i>)
     - elementy (přímí potomci) kontejneru

<span class="note"><a href="https://css-tricks.com/snippets/css/a-guide-to-flexbox/">Zdroj obrázku</a></span>

---

# 1. Grid kontejner: layout

- rodičovský element, který tvoří mřížku
- zvolíme strategii tvorby layoutu pomocí oblastí ***`grid-template-areas`***

```css
.container {
  display: grid;

  grid-template-columns: repeat(4, 1fr); /* 4 sloupcový layout */

  grid-template-areas: "header header header header"
                       "sidebar content content content";
                       /* vlastní pojmenování oblastí - tvorba samotného layoutu */
}
```

<pre class="code-render" default-style="

* {
  box-sizing: border-box;
}

.container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  text-align: center;
  align-items: center;
  justify-content: center;
}

.container > div {
  height: 100px;
  border: 2px solid black;
  display: flex;
  align-items: center;
  justify-content: center;
}

.header {
  color: blue;
}

.aside {
  color: green;
}

.article {
  color: red;
}

" resizable="true" style="height: 280px;">

<div class="container">
   <div class="header">header</div>
   <div class="header">header</div>
   <div class="header">header</div>
   <div class="header">header</div>
   <div class="aside">aside</div>
   <div class="article">article</div>
   <div class="article">article</div>
   <div class="article">article</div>
</div>

</pre>

=--

<!-- .slide: class="editor" -->

# Příklad

<div data-iframe="assets/examples/responsive/grid1.html"></div>

<div class="note"><a href="assets/examples/responsive/grid1.html">zdroj</a></div>

---

# 2. Položky grid kontejneru

<div style="float: right; width: 800px; z-index: 1; position: relative;">

```html
<div class="container">
  <header>header</header>
  <nav>nav</nav>
  <article>article</article>
</div>
```

</div>

```css
header {
  grid-area: header;
}

nav {
  grid-area: sidebar;
}

article {
  grid-area: content;
}
```

<pre class="code-render" default-style="

* {
  box-sizing: border-box;
}

.container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-areas: 'header header header header'
                       'sidebar content content content';
  text-align: center;
  align-items: center;
  justify-content: center;
}

.container > * {
  height: 100px;
  border: 2px solid lightgray;
  color: lightgray;
  display: flex;
  align-items: center;
  justify-content: center;
}

.container > div:nth-child(1) { grid-area: 1 / 1 / 2 / 2; }
.container > div:nth-child(2) { grid-area: 1 / 2 / 2 / 3; }
.container > div:nth-child(3) { grid-area: 1 / 3 / 2 / 4; }
.container > div:nth-child(4) { grid-area: 1 / 4 / 2 / 5; }
.container > div:nth-child(5) { grid-area: 2 / 1 / 3 / 2; }
.container > div:nth-child(6) { grid-area: 2 / 2 / 3 / 3; }
.container > div:nth-child(7) { grid-area: 2 / 3 / 3 / 4; }
.container > div:nth-child(8) { grid-area: 2 / 4 / 3 / 5; }

.container > header {
  grid-area: header;
  color: blue;
  border: 4px solid blue;
  background-color: #0000FF22;
  justify-content: left;
  padding: .2rem;
}

.container > nav {
  grid-area: sidebar;
  color: green;
  border: 4px solid green;
  background-color: #00FF0022;
  justify-content: left;
  padding: .2rem;
}

.container > article {
  grid-area: content;
  color: red;
  border: 4px solid red;
  background-color: #FF000022;
  justify-content: left;
  padding: .2rem;
}

" resizable="true" style="height: 280px;">

<div class="container">
  <div class="header">header</div>
  <div class="header">header</div>
  <div class="header">header</div>
  <div class="header">header</div>
  <div class="aside">aside</div>
  <div class="article">article</div>
  <div class="article">article</div>
  <div class="article">article</div>

  <header>header</header>
  <nav>nav</nav>
  <article>article</article>
</div>

</pre>

=--

<!-- .slide: class="editor" -->

# Příklad

<div data-iframe="assets/examples/responsive/grid2.html"></div>

<div class="note"><a href="assets/examples/responsive/grid2.html">zdroj</a></div>

---

# 3. Responzivní grid

```css
.container {
  display: grid;
  grid-template-columns: 1fr;
  grid-template-areas: "header"
                       "sidebar"
                       "content";
}
@media only screen and (min-width: 768px) {
  .container {
    grid-template-columns: repeat(2, 1fr);
    grid-template-areas: "header header"
                         "sidebar content";
  }
}
@media only screen and (min-width: 1200px) {
  .container {
    grid-template-columns: repeat(4, 1fr);
    grid-template-areas: "header header header header"
                         "sidebar content content content";
  }
}
```

---

# 3. Responzivní grid

<pre class="code-render" default-style="

* {
  box-sizing: border-box;
}

body {
  background-color: lightyellow;
}

.container {
  display: grid;
  grid-template-columns: 1fr;
  grid-template-areas: 'header'
                       'sidebar'
                       'content';
  justify-content: start;
  align-items: stretch;
  border: 4px solid blue;
  max-width: 1400px;
  margin: auto;
  background: white;
}

.container > * {
  border: 2px solid red;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1rem;
  padding-top: 2rem;
  position: relative;
}

.container > *::after {
  content: 'col: 100%';
  position: absolute;
  top: 10px;
  left: 10px;
  font-size: 24px;
  color: red;
  font-weight: normal;
}

header {
  text-align: center;
  grid-area: header;
}

h2 {
  margin: 0;
}

nav {
  grid-area: sidebar;
  background-color: bisque;
}

article {
  grid-area: content;
  background-color: bisque;
}

nav ul {
  align-self: start;
}

p {
  font-size: 20px;
  text-align: justify;
  margin: 0;
}

ul {
  margin: 0;
  font-size: 30px;
}

@media only screen and (min-width: 768px) {
  .container {
    grid-template-columns: repeat(2, 1fr);
    grid-template-areas: 'header header'
                         'sidebar content';
  }
  .container > header::after { content: 'col: 2/2' }
  .container > nav::after { content: 'col: 1/2' }
  .container > article::after { content: 'col: 1/2' }
}

@media only screen and (min-width: 1200px) {
  .container {
    grid-template-columns: repeat(4, 1fr);
    grid-template-areas: 'header header header header'
                         'sidebar content content content';
  }
  .container > header::after { content: 'col: 4/4' }
  .container > nav::after { content: 'col: 1/4' }
  .container > article::after { content: 'col: 3/4' }
}

" resizable="true" style="height: 800px;">

body
<div class="container">
  <header>
    <h2>
      Tworba webových stránek
    </h2>
  </header>
  <nav>
    <ul>
      <li>O předmětu</li>
      <li>Rozvrh</li>
      <li>Přednášky</li>
      <li>Cvičení</li>
      <li>Projekt</li>
    </ul>
  </nav>
  <article>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </article>
</div>

</pre>

<span class="note">💡 otestujte různé šířky příkladu</span>

=--

<!-- .slide: class="editor" -->

# Příklad

<div data-iframe="assets/examples/responsive/grid3.html"></div>

<div class="note"><a href="assets/examples/responsive/grid3.html">zdroj</a></div>

---

# Responzivní grid bez Media Queries

```css
.container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr) minmax(300px, 1fr));
  gap: .5rem;
}
```

<pre class="code-render" default-style="

* {
  box-sizing: border-box;
}

.container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr) minmax(300px, 1fr));
  gap: .5rem;
}

.container > div {
  border: 2px solid red;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: green;
}

.container > *:nth-child(odd) {
   color: black;
}

.container > *:nth-child(even) {
   color: gray;
}

p {
  font-size: 14px;
  text-align: justify;
  margin: 0;
  background-color: white;
}

" resizable="true" style="height: 500px;">

<div class="container">
  <div>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
  <div>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
  <div>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
  <div>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
</div>

</pre>

=--

<!-- .slide: class="editor" -->

# Příklad

<div data-iframe="assets/examples/responsive/grid4.html"></div>

<div class="note"><a href="assets/examples/responsive/grid4.html">zdroj</a></div>

---

# Shrnutí

- CSS Grid poskytuje pokročilé možnosti při rozmísťování elementů
  - oproti Flexbox umožňuje rozmísťovat ve 2D (řádky + sloupce) -- definice kompletního layoutu
  - není nutné definovat kontejner pro každý řádek
  - není nutné používat utility třídy v HTML dokumentu (*`row`*, *`col-`*)


