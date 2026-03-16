<!-- .slide: class="section" -->
 
<header>
    <h1>Grid systém: floats</h1>
</header>

---

# 1. Řádky

- na řádcích budou pozicovány bloky do sloupců -- třída ***.row***

<br>

- nutné řešit ***problémy plovoucích elementů:***
  - *clear: both* -- zalomení plovoucích (float) bloků za každým řádkem:
  ```css
  .row::after {
      content: "";
      clear: both;
  }
  ```
  - *overflow: hidden* -- některé sloupce řádku mohou mít menší výšku než je výsledná výška řádku
(sloupce dalšího řádku by mohly zasahovat do řádku předchozího):
  ```css
  .row {
      overflow: hidden;
  }
  ```

---

# 2. Sloupce

- do sloupců řádku budou organizovány jednotlivé elementy:

<br>

- nutné definovat třídy pro různě široké sloupce:
  ```css
  [class*="col-"] { float: left; }
  .col-1 { width: 25%; } /* 1/4 */
  .col-2 { width: 50%; } /* 2/4 */
  .col-3 { width: 75%; } /* 3/4 */
  .col-4 { width: 100%; } /* 4/4 */
  ```
  - vlastnost ***`float`*** způsobí obtékání elementů a tedy řazení vedle sebe 
  - vlastnost ***`width`*** určuje, kolik místa bude sloupec relativně zabírat na daném
řádku
  - počet sloupců může být takový, aby co nejlépe vystihoval daný problém
  - velmi často se využívá *12 sloupcový layout* (dobře dělitelné)

---

# 2. Sloupce: HTML

- elementům v HTML dokumentu budou nastaveny třídy dle požadovaného
rozmístění:

```html
<div id="content" class="row">
  <div id="sidebar" class="col-1">
    <!-- 1/4 -->
  </div>
  <div id="article" class="col-3">
    <!-- 3/4 -->
  </div>
</div>
```

<pre class="code-render" default-style="
.row {
  overflow: hidden;
  border: 4px solid blue;
}

.row::after {
  content: '';
  clear: both;
}

[class*='col-'] {
  float: left;
  height: 200px;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
}

#sidebar {
  background-color: lightblue;
}

#article {
  background-color: lightpink;
}

.col-1 { width: 25%; } /* 1/4 */
.col-2 { width: 50%; } /* 2/4 */
.col-3 { width: 75%; } /* 3/4 */
.col-4 { width: 100%; } /* 4/4 */

" resizable="true" style="height: 300px;">

<div id="content" class="row">
  <div id="sidebar" class="col-1">
    sidebar<br>1/4
  </div>
  <div id="article" class="col-3">
    article<br>3/4
  </div>
</div>

</pre>

<span class="note">💡 otestujte různé šířky příkladu</span>

=--

<!-- .slide: class="editor" -->

# Příklad

<div data-iframe="assets/examples/responsive/floats1.html"></div>

<div class="note"><a href="assets/examples/responsive/floats1.html">zdroj</a></div>

---

# 3. Breakpoints

- využití ***Media Queries*** pro bodů zlomu pro různé šířky oken (viewport) prohlížeče
  - např. [Bootstrap breakpoints](https://getbootstrap.com/docs/5.3/layout/breakpoints/), ...

```css
/* malé zařízení – implicitní zobrazení */
[class*="col-"] { float: left; width: 100%; }

/* středně velké (tablet) */
@media only screen and (min-width: 768px) {
  .col-md-1 { width: 25%; }
  .col-md-2 { width: 50%; }
  ...
}

/* velké (PC) */
@media only screen and (min-width: 1200px) {
  .col-lg-1 { width: 25%; }
  .col-md-2 { width: 50%; }
  ...
}
```

---

# 3. Breakpoints: HTML

- elementům v HTML dokumentu budou nastaveny třídy dle požadovaného rozmístění<br> pro jednotlivé skupiny šířek:

```html
<div id="content" class="row">
  <div id="sidebar" class="col-md-2 col-lg-1">
  </div>
  <div id="article" class="col-md-2 col-lg-3">
  </div>
</div>
```

<pre class="code-render" default-style="

.row {
  overflow: hidden;
  border: 4px solid blue;
}

.row::after {
  content: '';
  clear: both;
}

[class*='col-'] {
  float: left;
  width: 100%;
  height: 200px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
}

#sidebar {
  background-color: lightblue;
}

#article {
  background-color: lightpink;
}

[class*='col-']::after {
  content: '100%'
}

@media only screen and (min-width: 768px) {
  .col-md-1 { width: 25%; } /* 1/4 */
  .col-md-2 { width: 50%; } /* 2/4 */
  .col-md-3 { width: 75%; } /* 3/4 */
  .col-md-4 { width: 100%; } /* 4/4 */
  .col-md-1::after { content: '1/4' }
  .col-md-2::after { content: '2/4' }
  .col-md-3::after { content: '3/4' }
  .col-md-4::after { content: '4/4' }
}

@media only screen and (min-width: 1200px) {
  .col-lg-1 { width: 25%; } /* 1/4 */
  .col-lg-2 { width: 50%; } /* 2/4 */
  .col-lg-3 { width: 75%; } /* 3/4 */
  .col-lg-4 { width: 100%; } /* 4/4 */
  .col-lg-1::after { content: '1/4' }
  .col-lg-2::after { content: '2/4' }
  .col-lg-3::after { content: '3/4' }
  .col-lg-4::after { content: '4/4' }
}

" resizable="true" style="height: 300px;">

<div id="content" class="row">
  <div id="sidebar" class="col-lg-1 col-md-2">
    sidebar
  </div>
  <div id="article" class="col-lg-3 col-md-2">
    article
  </div>
</div>

</pre>

<span class="note">💡 otestujte různé šířky příkladu</span>

=--

<!-- .slide: class="editor" -->

# Příklad

<div data-iframe="assets/examples/responsive/floats2.html"></div>

<div class="note"><a href="assets/examples/responsive/floats2.html">zdroj</a></div>

---

# 4. Border a padding

- blokům pozicovaných do sloupců chceme často nastavit nějaký ***`padding`***, případně ***`border`***

<pre class="code-render" default-style="

.row {
  overflow: hidden;
  border: 4px solid blue;
}

.row::after {
  content: ' ';
  clear: both;
}

[class*='col-'] {
  float: left;
  border: 0px solid red;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: green;
}

.row > *:nth-child(odd) {
   color: black;
}

.row > *:nth-child(even) {
   color: gray;
}

p {
  font-size: 14px;
  text-align: justify;
  margin: 0;
  background-color: white;
}

#form {
  margin-bottom: .5rem;
}

input {
  font-size: 24px;
}

.col-1 { width: 25%; } /* 1/4 */
.col-2 { width: 50%; } /* 2/4 */
.col-3 { width: 75%; } /* 3/4 */
.col-4 { width: 100%; } /* 4/4 */

" resizable="true" style="height: 600px;">

<div id="form">
  border: <input id="border-width" type="number" min="0" value="0">
  padding: <input id="padding" type="number" min="0" value="0">
</div>

<div id="content" class="row">
  <div class="col-1">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
  <div class="col-1">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
  <div class="col-1">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
  <div class="col-1">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
</div>

<script>
  function setListener(type) {
    let elem = document.getElementById(type);
    if(elem) {
      elem.addEventListener("change", (e) => {
        let cols = document.querySelectorAll("[class*='col-']");
        for(let i = 0; i < cols.length; i++) {
          cols[i].style[type] = elem.value + "px";
        }
      });
    }
  }

  setListener("border-width");
  setListener("padding");
</script>

</pre>

<div style="text-align: center; margin-top: 4rem">

**skutečná šířka boxu** = <span style="color: lightgray">`margin`</span> + <span style="color: red">`border`</span> + <span style="color: green">`padding`</span> + `width`

</div>

=--

<!-- .slide: class="editor" -->

# Příklad

<div data-iframe="assets/examples/responsive/floats3.html"></div>

<div class="note"><a href="assets/examples/responsive/floats3.html">zdroj</a></div>

---

# 4. Border a padding: box-sizing

- vlastnost ***`box-sizing`*** umožní upravit rovnici box modelu

<br>

- hodnota ***`content-box`*** (by default):

<div class="box" style="text-align: center; margin-top: 4rem; padding: 1rem;">

**skutečná šířka boxu** = <span style="color: lightgray">`margin`</span> + <span style="color: red">`border`</span> + <span style="color: green">`padding`</span> + `width`

</div>

<br>

- hodnota ***`border-box`***:

<div class="box" style="text-align: center; margin-top: 4rem; padding: 1rem;">

  **skutečná šířka boxu** = <span style="color: lightgray">`margin`</span> + `width`<br>
  `width` = <span style="color: red">`border`</span> + <span style="color: green">`padding`</span> + <i>skutečná šířka obsahu</i> (dopočítá se)

</div>

<br>

- pozn: margin sloupců by měl být 0 (vlastnost nenastavujeme)

---

# 4. Border a padding: box-sizing

- nastavit všem elementům ***`box-sizing`*** na hodnotu ***`border-box`***:

```css
* {
  box-sizing: border-box;
}
```

- *`padding`* a *`border`* se bude *odpočítávat* od skutečné šířky boxu:

<pre class="code-render" default-style="

* {
  box-sizing: border-box;
}

.row {
  overflow: hidden;
  border: 4px solid blue;
}

.row::after {
  content: ' ';
  clear: both;
}

[class*='col-'] {
  float: left;
  border: 0px solid red;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: green;
}

.row > *:nth-child(odd) {
   color: black;
}

.row > *:nth-child(even) {
   color: gray;
}

p {
  font-size: 14px;
  text-align: justify;
  margin: 0;
  background-color: white;
}

#form {
  margin-bottom: .5rem;
}

input {
  font-size: 24px;
}

.col-1 { width: 25%; } /* 1/4 */
.col-2 { width: 50%; } /* 2/4 */
.col-3 { width: 75%; } /* 3/4 */
.col-4 { width: 100%; } /* 4/4 */

" resizable="true" style="height: 400px;">

<div id="form">
  border: <input id="border-width" type="number" min="0" value="0">
  padding: <input id="padding" type="number" min="0" value="0">
</div>

<div id="content" class="row">
  <div class="col-1">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
  <div class="col-1">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
  <div class="col-1">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
  <div class="col-1">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
</div>

<script>
  function setListener(type) {
    let elem = document.getElementById(type);
    if(elem) {
      elem.addEventListener("change", (e) => {
        let cols = document.querySelectorAll("[class*='col-']");
        for(let i = 0; i < cols.length; i++) {
          cols[i].style[type] = elem.value + "px";
        }
      });
    }
  }

  setListener("border-width");
  setListener("padding");
</script>

</pre>

=--

<!-- .slide: class="editor" -->

# Příklad

<div data-iframe="assets/examples/responsive/floats4.html"></div>

<div class="note"><a href="assets/examples/responsive/floats4.html">zdroj</a></div>

---

# 5. Margin

- často bývá vhodné nastavit nějaké ***okraje*** -- nastavujeme pro řádek ***`.row`*** nebo pro kontejner, který obaluje všechny řádky

```css
.row { max-width: 1400px; margin: auto; }
```

<pre class="code-render" default-style="

* {
  box-sizing: border-box;
}

body {
  background-color: lightyellow;
}

.row {
  overflow: hidden;
  border: 4px solid blue;
  max-width: 1400px;
  margin: auto;
  background: white;
}

.row::after {
  content: ' ';
  clear: both;
}

[class*='col-'] {
  float: left;
  border: 2px solid red;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1rem;
}

header {
  text-align: center;
}

h2 {
  margin: 0;
}

p {
  font-size: 20px;
  text-align: justify;
  margin: 0;
  background-color: white;
}

ul {
  margin: 0;
  font-size: 30px;
}

.col-1 { width: 25%; } /* 1/4 */
.col-2 { width: 50%; } /* 2/4 */
.col-3 { width: 75%; } /* 3/4 */
.col-4 { width: 100%; } /* 4/4 */

" resizable="true" style="height: 500px;">

body
<header id="content" class="row">
<h2 class="col-4">
  Tworba webových stránek
</h2>
</header>
<main id="content" class="row">
  <nav class="col-1">
    <ul>
      <li>O předmětu</li>
      <li>Rozvrh</li>
      <li>Přednášky</li>
      <li>Cvičení</li>
      <li>Projekt</li>
    </ul>
  </nav>
  <article class="col-3">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </article>
</main>

</pre>

<span class="note">💡 otestujte různé šířky příkladu</span>

=--

<!-- .slide: class="editor" -->

# Příklad

<div data-iframe="assets/examples/responsive/floats5.html"></div>

<div class="note"><a href="assets/examples/responsive/floats5.html">zdroj</a></div>

---

# Vše dohromady

<pre class="code-render" default-style="

* {
  box-sizing: border-box;
}

body {
  background-color: lightyellow;
}

.row {
  overflow: hidden;
  border: 4px solid blue;
  max-width: 1400px;
  margin: auto;
  background: white;
}

.row::after {
  content: ' ';
  clear: both;
}

[class*='col-'] {
  float: left;
  width: 100%;
  border: 2px solid red;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1rem;
  padding-top: 2rem;
  position: relative;
}

[class*='col-']::after {
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
}

h2 {
  margin: 0;
}

article, nav {
  background-color: bisque;
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
  .col-md-1 { width: 25%; } /* 1/4 */
  .col-md-2 { width: 50%; } /* 2/4 */
  .col-md-3 { width: 75%; } /* 3/4 */
  .col-md-4 { width: 100%; } /* 4/4 */
  .col-md-1::after { content: 'col: 1/4' }
  .col-md-2::after { content: 'col: 2/4' }
  .col-md-3::after { content: 'col: 3/4' }
  .col-md-4::after { content: 'col: 4/4' }
}

@media only screen and (min-width: 1200px) {
  .col-lg-1 { width: 25%; } /* 1/4 */
  .col-lg-2 { width: 50%; } /* 2/4 */
  .col-lg-3 { width: 75%; } /* 3/4 */
  .col-lg-4 { width: 100%; } /* 4/4 */
  .col-lg-1::after { content: 'col: 1/4' }
  .col-lg-2::after { content: 'col: 2/4' }
  .col-lg-3::after { content: 'col: 3/4' }
  .col-lg-4::after { content: 'col: 4/4' }
}

" resizable="true" style="height: 800px;">

body
<header id="content" class="row">
  <h2 class="col-lg-4 col-md-4">
    Tworba webových stránek
  </h2>
</header>
<main id="content" class="row">
  <nav class="col-lg-1 col-md-2">
    <ul>
      <li>O předmětu</li>
      <li>Rozvrh</li>
      <li>Přednášky</li>
      <li>Cvičení</li>
      <li>Projekt</li>
    </ul>
  </nav>
  <article class="col-lg-3 col-md-2">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </article>
</main>

</pre>

<span class="note">💡 otestujte různé šířky příkladu</span>

=--

<!-- .slide: class="editor" -->

# Příklad

<div data-iframe="assets/examples/responsive/floats6.html"></div>

<div class="note"><a href="assets/examples/responsive/floats6.html">zdroj</a></div>

---

# Shrnutí

- možnost, jak vytvořit Grid systém, když nebyl k dispozici Flexbox a Grid

<br>

- ***nevýhody***:
  - nutnost nastavovat vlastnosti `overflow` a `clear`
  - výška sloupce nemusí vyplnit výšku řádku
  - obecně jsou plovoucí elementy vhodné pro obtékání textu, nikoliv pro tvorbu layoutu
  - mezery mezi sloupci je nutné řešit pomocí `padding`

<br>

- řešení: ***Flexbox***