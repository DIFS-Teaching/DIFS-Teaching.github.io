<!-- .slide: class="section" -->

<header>
	<h1>Selektory</h1>
	<p>jednoduché, strukturované, pseudotřídy, pseudoselektory</p>
</header>

---

# Selektor

- operace, která vrátí ***množinu elementů***
  - nad vybranými elementy jsou aplikovány vlastnosti

- existují ***různé druhy selektorů***
  - *jednoduché* -- např. `p`, `.class`, `#id`, `[atribut]`
  - *strukturované* -- např. `div > p`, `a + b`)
  - *pseudotřídy* -- `:hover`
  - *pseudoelementy* - `::before`

- každý selektor má určitou ***váhu*** (`id` > `class` > `element`), která určuje, který styl má přednost
  - bude probráno na další přednášce

=--

<!-- .slide: class="editor" -->

# Přehled CSS selektorů

<div data-iframe="assets/examples/selectors/selectors.html"></div>

<div class="note"><a href="assets/examples/selectors/selectors.html">zdroj</a></div>

---

# Univerzální selektor: <code>*</code>

- aplikuje se na ***všechny elementy v dokumentu***

<pre class="code-render" default-style="
:not(.code-tag) {
  border: 4px solid green;
  background-color: #00FF0011;
}
" resizable="true" style="width: 50%; height: 700px; float: right; z-index: 1" tags="true">
&lt;body&gt;

<h1>&lt;h1&gt;ITW&lt;/h1&gt;</h1>

<h2>&lt;h2&gt;O předmětu&lt;/h2&gt;</h2>

<p>&lt;p&gt;Hello! You shall <i>&lt;i&gt;not&lt;/i&gt;</i> pass!.&lt;/p&gt;</p>

<h2>&lt;h2&gt;Přednášky&lt;/h2&gt;</h2>

<p>&lt;p&gt;...&lt;/p&gt;</p>

&lt;/body&gt;
</pre>

```css
* {
  border: 4px solid green;
  background-color: #00FF0011;
}
```

<span class="note">[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Universal_selectors)</span>

---

# Typový selektor: <code>tag</code>

- aplikuje se na všechny elementy ***daného jména***

<pre class="code-render" default-style="
h1 {
  border: 4px solid blue;
  background-color: lightblue;
}

h2 {
  border: 4px solid green;
  background-color: lightgreen;
}

i {
  border: 4px solid red;
  background-color: #ffcdcdff;
}
" resizable="true" style="width: 50%; height: 600px; float: right; z-index: 1" tags="true">
<h1>&lt;h1&gt;ITW&lt;/h1&gt;</h1>

<h2>&lt;h2&gt;O předmětu&lt;/h2&gt;</h2>

<p>&lt;p&gt;Hello! You shall <i>&lt;i&gt;not&lt;/i&gt;</i> pass!.&lt;/p&gt;</p>

<h2>&lt;h2&gt;Přednášky&lt;/h2&gt;</h2>

<p>&lt;p&gt;...&lt;/p&gt;</p>
</pre>

```css
h1 {
  border: 4px solid blue;
  background-color: lightblue;
}

h2 {
  border: 4px solid green;
  background-color: lightgreen;
}

i {
  border: 4px solid red;
  background-color: #ffcdcdff;
}
```

<span class="note">[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Type_selectors)</span>

---

# Třída elementů: <code>.class</code>

- aplikuje se na všechny elementy ***dané třídy***
  - v jedné třídě může být více elementů, jeden element může být ve více třídách

<pre class="code-render" default-style="
.box {
  border: 4px solid blue;
  background-color: lightblue;
}

h2.box {
  border: 4px solid green;
  background-color: lightgreen;
}

*.red {
  color: red;
}
" resizable="true" style="width: 50%; height: 650px; float: right; z-index: 1" tags="true">
<h1 class="box">&lt;h1 class="box"&gt;ITW&lt;/h1&gt;</h1>

<h2>&lt;h2&gt;O předmětu&lt;/h2&gt;</h2>

<p>&lt;p&gt;Hello! You shall <i class="red box">&lt;i class="red box"&gt;not&lt;/i&gt;</i> pass!.&lt;/p&gt;</p>

<h2 class="box red">&lt;h2 class="box red"&gt;Přednášky&lt;/h2&gt;</h2>

<p class="box">&lt;p class="box"&gt;...&lt;/p&gt;</p>
</pre>

```css
.box {
  border: 4px solid blue;
  background-color: lightblue;
}

h2.box {
  /* přetížení .box */
  border: 4px solid green;
  background-color: lightgreen;
}

/* to stejné jako .red */
*.red {
	color: red;
}
```

<span class="note">[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Type_selectors)</span>

---

# Identifikátor elementu: <code>#id</code>

- aplikuje se na unikátní element ***daného identifikátoru***
  - pokud jich bude ***chybně*** více, aplikuje se na všechny výskyty

<pre class="code-render" default-style="
#unique {
  border: 4px solid blue;
  background-color: lightblue;
}

i#unique {
  color: red;
}
" resizable="true" style="width: 50%; height: 650px; float: right; z-index: 1" tags="true">
<h1 id="unique">&lt;h1 id="unique"&gt;ITW&lt;/h1&gt;</h1>

<h2>&lt;h2&gt;O předmětu&lt;/h2&gt;</h2>

<p>&lt;p&gt;Hello! You shall <i id="unique">&lt;i id="unique"&gt;not&lt;/i&gt;</i> pass!.&lt;/p&gt;</p>

<h2>&lt;h2&gt;Přednášky&lt;/h2&gt;</h2>

<p>&lt;p&gt;...&lt;/p&gt;</p>
</pre>

```css
#unique {
  border: 4px solid blue;
  background-color: lightblue;
}

/* obecně nedává moc smysl,
   jelikož by se dle
   HTML specifikace
   mělo jednat o unikátní
   element v dokumentu */
i#unique {
  color: red;
}
```

<span class="note">[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/ID_selectors)</span>

---

# Atribut elementů: <code>[atribut]</code>

- aplikuje se na všechny elementy jejichž atributy splňují podmínku

<pre class="code-render" default-style="
[title] {
  color: red;
}

h1[title='Web design'] {
  border: 4px solid blue;
  background-color: lightblue;
}

h2[title*='eb'] {
  border: 4px solid green;
  background-color: lightgreen;
}
" resizable="true" style="width: 50%; height: 650px; float: right; z-index: 1" tags="true">
<h1 title="Web design">&lt;h1 title="Web design"&gt;ITW&lt;/h1&gt;</h1>

<h2 title="design">&lt;h2 title="design"&gt;O předmětu&lt;/h2&gt;</h2>

<p>&lt;p&gt;Hello! You shall <i title="design">&lt;i title="design"&gt;not&lt;/i&gt;</i> pass!.&lt;/p&gt;</p>

<h2 title="Web design">&lt;h2 title="Web design"&gt;Přednášky&lt;/h2&gt;</h2>

<p>&lt;p&gt;...&lt;/p&gt;</p>
</pre>

```css
[title] {
  color: red;
}

h1[title='Web design'] {
  border: 4px solid blue;
  background-color: lightblue;
}

h2[title*='eb'] {
  border: 4px solid green;
  background-color: lightgreen;
}
```

- <em>*=</em> podřetězec, *^=* prefix, *$=* suffix
- *~=* podřetězec oddělený bílými znaky
- *|=* hodnota začíná daným řetězcem nebo za řetězcem následuje pomlčka


<span class="note">[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors)</span>

---

# Strukturované selektory

- složený selektor: ***<code>s1 op s2</code>***, kde op je následující operátor

<pre class="code-render" default-style="
article p {
  color: red;
}

article > p {
  border: 4px solid blue;
}

div ~ p {
    background-color: lightblue;
}

div + p {
    font-style: italic;
	font-weight: bold;
}
" resizable="true" style="width: 50%; height: 750px; float: right; z-index: 1" tags="true">
<article>
&lt;article&gt;

<div class="lectures">
&nbsp;&lt;div class="lectures"&gt;

<p>&nbsp;&nbsp;&lt;p&gt;Web&lt;/p&gt;</p>
<p>&nbsp;&nbsp;&lt;p&gt;HTML&lt;/p&gt;</p>
<p>&nbsp;&nbsp;&lt;p&gt;CSS&lt;/p&gt;</p>

&nbsp;&lt;/div&gt;
</div>

<p>&nbsp;&lt;p&gt;You shall not pass!.&lt;/p&gt;</p>

<p>&nbsp;&lt;p&gt;Hello!&lt;/p&gt;</p>

&lt;/article&gt;
</article>

</pre>

```css
/* potomci */
article p {
  color: red;
}

/* přímí potomci */
article > p {
  border: 4px solid blue;
}

/* následující sourozeneci */
div ~ p {
    background-color: lightblue;
}

/* přímo následující sourozenci */
div + p {
    font-style: italic;
	font-weight: bold;
}
```

---

# Seskupování

- více pravidel se stejnými vlastnostmi můžeme seskupit do jednoho pravidla

```css
h1 {
  color: red;
  font-weight: bold;
}

section h2 {
  color: red;
}
```

- seskupení pro vlastnost *`color: red`*

```css
h1, section h2 {
  color: red;
}

h1 {
  font-weight: bold;
}
```

---

# Pseudotřídy

- speciální selektory začínající *`:`*, které cílí na *stav* elementu, jeho *umístění* nebo *logický kontext*:

  - ***stavové*** (interakce uživatele)
    - `:hover`, `:active`, `:focus`, `:target`, ...
  - ***formulářové stavy***
    - `:enabled`, `:checked`, `:valid`, `:required`, ...
  - ***strukturální*** (pozice v DOM)
     - `:root`, `:first-child`, `:nth-child(n)`, `:first-of-type`, ...
  - ***logické***
     - `:not`, `:is`, `:where`, `:has`, ...
  - ***ostatní*** (jazykové, odkazy a další speciální...)
    - `:lang`, `:dir`, `:link`, `:visited`, ...

---

# Pseudotřídy: stavové

<pre class="code-render" default-style="
article :not(.code-tag):hover {
  color: blue;
}

article :not(.code-tag):focus {
  border: 6px solid green;
}

article :not(.code-tag):active {
  color: red;
}

body :not(.code-tag):target {
  border: 4px solid orange;
}

input {
  font-size: 1rem;
}

h2, p, input {
  margin: 0.5rem;
}

" resizable="true" style="width: 50%; height: 650px; float: right; z-index: 1" tags="true">
<a href="#about">&lt;a href="#about"&gt;O předmětu&lt;/a&gt;</a>
<br>

<article id="about">
&lt;article id="about"&gt;

<h2 id="about">&lt;h2&gt;O předmětu&lt;/h2&gt;</h2>

<p>&lt;p&gt;Hello! You shall not pass!.&lt;/p&gt;</p>

&nbsp;&nbsp;&lt;input type="text" placeholder="Name"&gt;
<input type="text" placeholder="Name"></input><br>
&nbsp;&nbsp;&lt;/input&gt;<br>
&nbsp;&nbsp;&lt;input type="text" placeholder="Surname"&gt;
<input type="text" placeholder="Surname"></input><br>
&nbsp;&nbsp;&lt;/input&gt;<br>

&lt;/article&gt;
</article>

</pre>

```css
/* najetí myší */
article *:hover {
  color: blue;
}

/* kliknutí a držení myši */
article *:active {
  color: red;
}

/* aktivní pomocí klávesy TAB */
article *:focus {
  border: 6px solid green;
}

/* kliknutí na odkaz
   odkazující na element */
body *:target {
  border: 4px solid orange;
}
```

---

# Pseudotřídy: formulářové stavy

<pre class="code-render" default-style="
input {
  font-size: 1rem;
  border: 4px solid gray;
}

input:required {
  border: 6px solid tomato;
}

input:valid {
  background-color: lightgreen;
}

input:invalid {
  background-color: #FFCCCB;
}

input:disabled ~ label {
  font-style: italic;
}

input[type='checkbox']:checked ~ label {
  color: red;
}

input[type='checkbox'] {
  width: 30px;
  height: 30px;
}
" resizable="true" style="width: 50%; height: 850px; float: right; z-index: 1" tags="true">


&lt;input type="text" placeholder="Name"&gt;<br>
<input type="text" placeholder="Name" required></input><br>
&lt;/input&gt;<br><br>

&lt;input type="text" placeholder="Surname"&gt;<br>
<input type="text" placeholder="Surname"></input><br>
&lt;/input&gt;<br><br>

&lt;input type="number" min="1" placeholder="Age"&gt;<br>
<input type="number" min="1" placeholder="Age" required></input><br>
&lt;/input&gt;<br><br>

&lt;input id="soul" type="checkbox"&gt;<br>
<input id="soul" type="checkbox" disabled checked></input><br>
&lt;/input&gt;<br>
&lt;label for="soul"&gt;<br>
<label for="soul">My soul belongs to FIT<label><br>
&lt;/label&gt;<br>

</pre>

```css
input:required {
  border: 6px solid tomato;
}

input:valid {
  background-color: lightgreen;
}

input:invalid {
  background-color: #FFCCCB;
}

input:disabled + label {
  font-style: italic;
}

input[type='checkbox']:checked
  + label {
  color: red;
}
```

---

# Pseudotřídy: strukturální

<pre class="code-render" default-style="
:root {
  border: 4px solid red;
}

p:nth-of-type(1) {
  border: 4px solid blue;
}

p:nth-child(1) {
  background-color: lightblue;
}

h2, p, div {
  margin: 0.5rem 0;
}
" resizable="true" style="width: 50%; height: 600px; float: right; z-index: 1" tags="true">
&lt;article&gt;
<article>

<h2>&nbsp;&nbsp;&lt;h2&gt;O předmětu&lt;/h2&gt;</h2>

<p>&nbsp;&nbsp;&lt;p&gt;Hello! You shall not pass!.&lt;/p&gt;</p>

&nbsp;&nbsp;&lt;div class="lectures"&gt;
<div class="lectures">
<p>&nbsp;&nbsp;&nbsp;&nbsp;&lt;p&gt;Web&lt;/p&gt;</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&lt;p&gt;HTML&lt;/p&gt;</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&lt;p&gt;CSS&lt;/p&gt;</p>
</div>
&nbsp;&nbsp;&lt;/div&gt;
</article>
&lt;/article&gt;

</pre>

```css
/* <html element> */
:root { border: 4px solid red; }

p:nth-of-type(1) {
  border: 4px solid blue;
}
p:nth-child(1) {
  background-color: lightblue;
}
```

- ***pořadí uzlu v rodiči:***
  - `:first-child`, `:last-child`, `:only-child`, `:nth-child(n)`, `:nth-last-child(n)`
- ***pořadí typu v rodiči:***
  - `:first-of-type`, `:last-of-type`, `:only-of-type`,<br> `:nth-of-type(n)`, `:nth-last-of-type(n)`

---

# Pseudotřídy: logické

<pre class="code-render" default-style="

*:has(h2) {
  border: 4px solid blue;
}

:not(article):has(> p) {
  border: 4px solid green;
}

article > :is(h2, p) {
  color: red;
}

:where(article, div) > :not(:is(p, div, .code-tag)) {
  border: 4px solid orange;
}

" resizable="true" style="width: 40%; height: 700px; float: right; z-index: 1; margin-left: 1rem;" tags="true">
<article>
&lt;article&gt;

<h2>&nbsp;&nbsp;&lt;h2&gt;O předmětu&lt;/h2&gt;</h2>

<p>&nbsp;&nbsp;&lt;p&gt;Hello! You shall not pass!.&lt;/p&gt;</p>

<div class="lectures">
&nbsp;&nbsp;&lt;div class="lectures"&gt;
<p>&nbsp;&nbsp;&nbsp;&nbsp;&lt;p&gt;Web&lt;/p&gt;</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&lt;p&gt;HTML&lt;/p&gt;</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&lt;p&gt;CSS&lt;/p&gt;</p>
&nbsp;&nbsp;&lt;/div&gt;
</div>

&lt;/article&gt;
</article>

</pre>

```css
/* všechny elem., které obsahují h2 */
*:has(> h2) {
  border: 4px solid blue;
}

/* všechny elem. mimo artcile,
   které obsahují p jako přímého potomka */
:not(article):has(> p) {
  border: 4px solid green;
}

/* všechny elem. h2 a p,
   které jsou v article jako přímí potomci */
article > :is(h2, p) {
  color: red;
}

/* všechny elem. mimo p a div, které
   jsou v article nebo div jako přímí potomci */
:where(article, div) > :not(:is(p, div)) {
  border: 4px solid orange;
}
```

<span class="note">priority a rozdíly mezi `:is` a `:where` v další přídnášce</span>

---

# Pseudotřídy: další specifické...

- *`:lang()`* -- rozlišení dle jazyku (atribut `lang`)
- *`:dir(rtl)`* -- elementy s textovým směrem right-to-left (např. arabština, hebrejština)
- *`:link`* -- nenavštívené odkazy
- *`:visited`* -- odkazy, které uživatel navštívil
- *`:any-link`* -- všechny odkazy (`:link` i `:visited`)
- a spousta dalších...

<br>

- více v **[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_selectors#selectors)**...

---

# Pseudoelementy

- součást CSS selektorů (není přímo CSS selektor) začínající *`::`*, která umožní cílit na určitou část elementu, *i když pro ni v HTML neexistuje samostatný tag*:
  - ***textové*** (zaměřují se na část textu)
    - `::first-line`, `::first-letter`, `::selection`, ...
  - ***vstupní a formulářové*** (specifické pro `<input>`, `<textarea>` a formuláře.)
    - `::placeholder`, `::file-selector-button`,, `::cue`, ...
  - ***obsahové*** (k přidávání nebo manipulaci s obsahem)
    - `::before`, `::after`
  - ***ostatní speciální***
    - [`::marker`](https://developer.mozilla.org/en-US/docs/Web/CSS/::marker) -- styl odrážek u seznamů `<li>`
    - [`::cue`](https://developer.mozilla.org/en-US/docs/Web/CSS/::cue) -- styl titulků v `<track>` u `<video>`
    - ...

---

# Pseudoelementy: textové

<pre class="code-render" default-style="

/* První řádek textu bude tučný a modrý */
p::first-line {
  font-weight: bold;
  color: blue;
}

/* První písmeno bude obrovské a červené */
p::first-letter {
  font-size: 3em;
  color: red;
  float: left;
  margin-right: 5px;
}

/* Text vybraný uživatelem bude s pozadím žlutým a textem černým */
p::selection {
  background: yellow;
  color: black;
}

" resizable="true" style="width: 40%; height: 400px; float: right; z-index: 1; margin-left: 1rem;" tags="true">

&lt;p&gt;<p>You shall not pass!. One ring to rule them all, one ring to find them, One ring to bring them all and in the darkness bind them.</p>&lt;/p&gt;

</pre>

```css
/* První řádek textu bude tučný a modrý */
p::first-line {
  font-weight: bold;
  color: blue;
}

/* První písmeno bude obrovské a červené */
p::first-letter {
  font-size: 3em;
  color: red;
  float: left;
  margin-right: 5px;
}

/* Text vybraný uživatelem bude
   s pozadím žlutým a textem černým */
p::selection {
  background: yellow;
  color: black;
}
```

---

# Pseudoelementy: vstupní a formulářové

<pre class="code-render" default-style="
input {
  font-size: 1rem;
}

input::placeholder {
  color: SandyBrown;
  font-style: italic;
}

/* File input button – styl tlačítka */
input[type='file']::file-selector-button {
  background-color: #4CAF50;
  color: white;
  padding: 5px 10px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

input[type='file']::file-selector-button:hover {
  background-color: #45a049;
}

" resizable="true" style="width: 35%; height: 850px; float: right; z-index: 1" tags="true">

<h2>&lt;h2&gt;Projekt 1&lt;/h2&gt;</h2>

&lt;input type="text" placeholder="Name"&gt;<br>
<input type="text" placeholder="Login" required></input><br>
&lt;/input&gt;<br><br>

&lt;input type="file"<br>
<input type="file" placeholder="File"></input><br>
&lt;/input&gt;<br>

</pre>

```css
input::placeholder {
  color: SandyBrown;
  font-style: italic;
}

/* styl tlačítka */
input[type="file"]::file-selector-button {
  background-color: #4CAF50;
  color: white;
  padding: 5px 10px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

input[type="file"]::file-selector-button:hover {
  background-color: #45a049;
}
```

---

# Pseudoelementy: obsahové

- možnost přidat nové elementy do DOM

<pre class="code-render" default-style="

span:not(.code-tag)::before {
  content: '&#x1F9D9;'
}

span:not(.code-tag)::after {
  content: ' ';
  display: inline-block;
  width: 100px;
  height: 100px;
  background-image: url('https://www.fit.vut.cz/study/course/ITW/public/assets/gandalf.png');
  background-size: contain;
  background-repeat: no-repeat;
  vertical-align: middle;
}

" resizable="true" style="width: 45%; height: 200px; float: right; z-index: 1; margin-left: 1rem;" tags="true">

&lt;span&gt;<span>You shall not pass!.</span>&lt;/span&gt;

</pre>

```css
span:not(.code-tag)::before {
  content: '&#x1F9D9;'
}

span:not(.code-tag)::after {
  content: ' ';
  display: inline-block;
  width: 100px;
  height: 100px;
  background-image: url('gandalf.png');
  background-size: contain;
  background-repeat: no-repeat;
  vertical-align: middle;
}
```

- součástí elementu (první nebo poslední potomek)
- vždy je nutné, aby pravidlo obsahovalo vlastnost ***`content`***
