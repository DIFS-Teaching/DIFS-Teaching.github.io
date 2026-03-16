<!-- .slide: class="section" -->

<header>
	<h1>Vybrané blokové elementy</h1>
	<p>struktura dokumentu, nadpisy, textové bloky, seznamy, tabulky, (média, formuláře)</p>
</header>

---

# Základní struktura obsahu

- **`article`** -- článek, příspěvek (samostatně použitelná část obsahu)
- **`section`** -- kapitola článku, příspěvku, apod.
- **`aside`** -- část, která se jen vzdáleně vztahuje k hlavnímu obsahu
- **`header`** -- záhlaví dokumentu, článku, apod.
- **`footer`** -- zápatí
- **`main`** -- hlavní obsah stránky (unikátní)
- **`nav`** -- část obsahující navigaci
- **`div`** -- obecný blok bez dalšího významu (pro skriptování, styly, apod.)

=--

<!-- .slide: class="editor" -->

# Základní struktura obsahu

<div data-iframe="assets/examples/html/html-structure.html"></div>

<div class="note"><a href="assets/examples/html/html-structure.html">zdroj</a></div>

---

# Nadpisy: h1 - h6

<pre class="code-render" default-style="" resizable="true" style="width: 50%; height: 700px; float: right; z-index: 1">
<h1>Nadpis 1. úrovně</h1>
<h2>Nadpis 2. úrovně</h2>
<h3>Nadpis 3. úrovně</h3>
<h4>Nadpis 4. úrovně</h4>
<h5>Nadpis 5. úrovně</h5>
<h6>Nadpis 6. úrovně</h6>
</pre>

```html
<h1>Nadpis 1. úrovně</h1>
<h2>Nadpis 2. úrovně</h2>
<h3>Nadpis 3. úrovně</h3>
<h4>Nadpis 4. úrovně</h4>
<h5>Nadpis 5. úrovně</h5>
<h6>Nadpis 6. úrovně</h6>
```

- elementy základní struktury dokumentu zpravidla vyžadují nadpis

---

# Textové bloky

<pre class="code-render" default-style="" resizable="true" style="width: 45%; height: 500px; float: right; z-index: 1">
<p>
  Toto je odstavec textu.
  Odstavce se používají
  pro běžný obsah.
</p>

<blockquote>
  „Toto je citát, který je zobrazen
  jako samostatný blok.“
</blockquote>

<address>
  Kontakt: Jan Novák
</address>
</pre>

```html
<p>
  Toto je odstavec textu.
  Odstavce se používají
  pro běžný obsah.
</p>

<blockquote>
  „Toto je citát, který je zobrazen
  jako samostatný blok.“
</blockquote>

<address>
  Kontakt: Jan Novák
</address>
```

- ukončující značka `</p>` není povinná (*nedoporučuje se*)
  - odstavec ukončen začátkem dalšího blokového elementu
- uvnitř `p` a `address` mohou být pouze řádkové elementy

---

# Textové bloky: `<details>`

<pre class="code-render" default-style="" resizable="true" style="width: 45%; height: 500px; float: right; z-index: 1">
<details>
  <summary>Tyrion Lannister</summary>
  <p>Drinks wine like it’s water, talks like every word costs gold, and somehow survives when everyone else doesn’t.</p>
</details>

<details open>
  <summary>Hodor</summary>
  <p>Can carry a child, a sled, and the emotional weight of his own backstory — all while saying just one word: "Hodor".</p>
</details>
</pre>

```html
<details>
  <summary>Tyrion Lannister</summary>
  <p>Drinks wine like it’s water, talks like every word costs gold, and somehow survives when everyone else doesn’t.</p>
</details>

<details>
  <summary>Hodor</summary>
  <p>Can carry a child, a sled, and the emotional weight of his own backstory — all while saying just one word: "Hodor".</p>
</details>
```

- ***`details`***
  - může obsahovat libovolné HTML (text, obrázky, seznamy, formuláře…).
  - první potomek musí být ***`summary`*** -- mění stav (atribut *`open`*)

---

# Předformátovaný text

- zachovává formátování pomocí mezer a konce řádku
- obvykle neproporcionálním písmem
- CSS vlastnost: `white-space: pre;`


```html
<pre>
  Toto je předformátovaný text.
     Zachovává    zalomení  řádků a mezery
Značky se ale interpretují <b>normálně</b>.
</pre>
```

<pre class="code-render" default-style="" resizable="true" style="height: 220px;">  
<pre>
  Toto je předformátovaný text.
     Zachovává    zalomení  řádků a mezery
Značky se ale interpretují <b>normálně</b>.
</pre>
</pre>

---

# Číslovaný a nečíslovaný seznam

<pre class="code-render" default-style="" resizable="true" style="width: 45%; height: 500px; float: right; z-index: 1">
<ul>
  <li>Red team
    <ol>
      <li>Ice Truck Killer</li>
      <li>The Trinity Killer</li>
      <li>The Doomsday Killer</li>
    </ol>
  </li>
  <li>Blue team
    <ol>
      <li>Little Chino</li>
      <li>The Bay Harbor Butcher</li>
    </ol>
  </li>
</ul>
</pre>

```html
<ul>
  <li>Red team
    <ol>
      <li>Ice Truck Killer</li>
      <li>The Trinity Killer</li>
      <li>The Doomsday Killer</li>
    </ol>
  </li>
  <li>Blue team
    <ol>
      <li>Little Chino</li>
      <li>The Bay Harbor Butcher</li>
    </ol>
  </li>
</ul>
```

- seznam ***`<ul>`*** (*<i>unordered list</i>*) a ***`<ol>`*** (*<i>ordered list</i>*) může obsahovat jen elementy ***`<li>`***
- položka seznamu ***`<li>`*** (*<i>list item</i>*) může obsahovat libovolné blokové i řádkové elementy
  - zanoření seznamů

---

# Definiční seznam

<pre class="code-render" default-style="" resizable="true" style="width: 40%; height: 500px; float: right; z-index: 1">
<dl>
  <dt>Ice Truck Killer</dt>
  <dd>
     Brian Moser, známý pro rozřezávání
     a aranžování těl.
  </dd>

  <dt>The Doomsday Killer</dt>
  <dd>
    Travis Marshall, vraždy inspirované
    biblickou knihou Zjevení.
  </dd>
</dl>
</pre>

```html
<dl>
  <dt>Ice Truck Killer</dt>
  <dd>
     Brian Moser, známý pro rozřezávání
     a aranžování těl.
  </dd>

  <dt>The Doomsday Killer</dt>
  <dd>
    Travis Marshall, vraždy inspirované
    biblickou knihou Zjevení.
  </dd>
</dl>
```

  - seznam ***`<dl>`*** (*<i>definition list</i>*) může obsahovat jen elementy ***`<dt>`*** a ***`<dd>`*** (v libovolné posloupnosti)
  - termín ***`<dt>`*** (*<i>definition term</i>*) nemůže obsahovat sekce a nadpisy
  - definice ***`<dd>`*** (*<i>definition description</i>*) může obsahovat libovolné blokové i řádkové elementy

---

# Tabulka

<pre class="code-render" default-style="" resizable="true" style="width: 50%; height: 500px; float: right; z-index: 1">
<table>
  <tr>
    <th>First Name</th>
    <th>Last Name</th>
    <th>Residence</th>
  </tr>
  <tr>
    <td>Jon</td>
    <td>Snow</td>
    <td>Winterfell</td>
  </tr>
  <tr>
    <td>Tyrion</td>
    <td>Lannister</td>
    <td>King's Landing</td>
  </tr>
</table>
</pre>

```html
<table>
  <tr>
    <th>First Name</th>
    <th>Last Name</th>
    <th>Residence</th>
  </tr>
  <tr>
    <td>Jon</td>
    <td>Snow</td>
    <td>Winterfell</td>
  </tr>
  <tr>
    <td>Tyrion</td>
    <td>Lannister</td>
    <td>King's Landing</td>
  </tr>
</table>
```

- tabulka ***`<table>`*** je organizována po řádcích ***`<tr>`*** (*<i>table row</i>*)
- řádky ***`<tr>`*** obsahují buňky ***`<td>`*** (*<i>table data</i>*) a ***`<th>`*** (*<i>table header</i>*)

---

# Tabulka: styl

<pre class="code-render" default-style="
table {
  border: 2px solid blue;
}

td {
  border: 2px solid green;
}

th {
  border: 2px solid red;
}

/* sloučení okrajů  */
table:nth-of-type(2) {
  border-collapse: collapse;
}

" resizable="true" style="width: 50%; height: 500px; float: right; z-index: 1">
<table>
  <tr>
    <th>First Name</th>
    <th>Last Name</th>
    <th>Residence</th>
  </tr>
  <tr>
    <td>Jon</td>
    <td>Snow</td>
    <td>Winterfell</td>
  </tr>
  <tr>
    <td>Tyrion</td>
    <td>Lannister</td>
    <td>King's Landing</td>
  </tr>
</table>

<br><br>

<table>
  <tr>
    <th>First Name</th>
    <th>Last Name</th>
    <th>Residence</th>
  </tr>
  <tr>
    <td>Jon</td>
    <td>Snow</td>
    <td>Winterfell</td>
  </tr>
  <tr>
    <td>Tyrion</td>
    <td>Lannister</td>
    <td>King's Landing</td>
  </tr>
</table>
</pre>

```css
table {
  border: 2px solid blue;
}

td {
  border: 2px solid green;
}

th {
  border: 2px solid red;
}

/* sloučení okrajů */
table:nth-of-type(2) {
  border-collapse: collapse;
}
```

- v základním zobrazení tabulka nemá vizuální okraje

<span class="note">více v přednášce CSS</span>

---

# Tabulka: sloučení buněk

<pre class="code-render" default-style="
table {
s
  border-collapse: collapse;
}

td {
  border: 2px solid black;
}

th {
  border: 2px solid black;
}
" resizable="true" style="width: 40%; height: 500px; float: right; z-index: 1">
<table>
  <tr>
    <th>First Name</th>
    <th>Last Name</th>
    <th>Residence</th>
  </tr>
  <tr>
    <td>John</td>
    <td>Snow</td>
    <td class="join" rowspan="2">Winterfell</td>
  </tr>
  <tr>
    <td class="join" colspan="2">Hodor</td>
  </tr>
</table>
</pre>

```html
<table>
  <tr>
    <th>First Name</th>
    <th>Last Name</th>
    <th>Residence</th>
  </tr>
  <tr>
    <td>John</td>
    <td>Snow</td>
    <td rowspan="2">Winterfell</td>
  </tr>
  <tr>
    <td colspan="2">Hodor</td>
  </tr>
</table>
```

- ***`colspan="n"`*** -- šířka ve sloupcích
- ***`rowspan="n"`*** -- výška v řádcích
- aplikuje se na ***`<td>`*** nebo ***`<th>`***, nikoliv **`<tr>`**

---

# Tabulka: sémantické elementy

```html
<table>
  <thead>
    <!-- skupina řádků s hlavičkou sloupců -->
  <thead>
  <tbody>
    <!-- skupina řádků s hlavním obsahem -->
  </tbody>
  <tfoot>
    <!-- skupina řádků se souhrnem nebo poznámkami -->
  <tfoot>
</table>
```

- volitelné elementy pro zdůraznění sémantiky, vizuálně se neprojeví
  - pokud nejsou uvedené, prohlížeč v DOM umístí všechny řádky do ***`<tbody>`***
- ***`<tfoot>`*** je možné uvést před ***`<tbody>`***, prohlížeče umístí pod
  - původně (v HTML 4) se tím optimalizovalo načítání tabulek

---

# Tabulka: deklarace sloupců

<pre class="code-render" default-style="
table, td, th {
  border: 2px solid black;
}
" resizable="true" style="width: 40%; height: 400px; float: right; z-index: 1; margin: 2rem">
<table>
  <!-- skupina sloupců -->
  <colgroup style="background-color: yellow;">
    <col
      span="2" 
      style="background-color: lightblue">
    <col style="background-color: lightgreen">
    <col>
  </colgroup>
  <tr>
    <th>First Name</th>
    <th>Last Name</th>
    <th>Residence</th>
    <th>#</th>
  </tr>
  <tr>
    <td>Jon</td>
    <td>Snow</td>
    <td>Winterfell</td>
    <td>1</td>
  </tr>
  <tr>
    <td>Tyrion</td>
    <td>Lannister</td>
    <td>King's Landing</td>
    <td>2</td>
  </tr>
</table>
</pre>

```html
<table>
  <colgroup style="background-color: yellow;">
    <col
      span="2" 
      style="background-color: lightblue">
    <col style="background-color: lightgreen">
    <col>
  </colgroup>
  <tr>
    <!-- tabulka... -->
</table>
```

- slouží pro hromadnou specifikaci vlastností pro sloupce
  - ***`<col>`*** -- jeden nebo více sloupců se společnými atributy
  - ***`<colgroup>`*** -- skupina sloupců (strukturální)
- definice sloupců ovlivňují pouze strukturu, nikoliv obsah
- pokud není definované, celá tabulka se považuje za jedinou skupinu sloupců

---

# Tabulka: popisek tabulky

<pre class="code-render" default-style="
table, td, th {
  border: 2px solid black;
}

/* pozice popisku */
caption {
  caption-side: bottom;
}
" resizable="true" style="width: 50%; height: 300px; float: right; z-index: 1">
<table>
  <caption>
    Game of Thrones Characters
  </caption>
  <tr>
    <th>First Name</th>
    <th>Last Name</th>
    <th>Residence</th>
  </tr>
  <tr>
    <td>Jon</td>
    <td>Snow</td>
    <td>Winterfell</td>
  </tr>
  <tr>
    <td>Tyrion</td>
    <td>Lannister</td>
    <td>King's Landing</td>
  </tr>
</table>
</pre>

```html
<table>
  <caption>
    Game of Thrones Characters
  </caption>
  ...
<table>
```

```css
/* pozice popisku */
caption {
  caption-side: bottom;
}
```

- ***`<caption>`*** musí být prvním potomkem ***`<table>`***
- pozice popisku je implicitne nad tabulkou
  - změna pomocí CSS vlastnosti *`caption-side: top|bottom;`*

<span class="note">více v přednášce CSS</span>

---

# Média: `<figure>`

<pre class="code-render" default-style="" resizable="true" style="width: 30%; height: 600px; float: right; z-index: 1; margin: 2rem">
<figure>
  <img src="https://www.fit.vut.cz/study/course/ITW/public/assets/tyrion.jpg" alt="Tyrion"
    height="450">
  <figcaption>Tyrion -- he knows things</figcaption>
</figure>
</pre>

```html
<figure>
  <img src="tyrion.jpg" alt="Tyrion" height="450">
  <figcaption>Tyrion -- he knows things</figcaption>
</figure>
```

- ***`figure`*** -- blok obsahující médium (obrázek, video) s popiskem
  - obrázky: *`<img>`*, *`<svg>`*, *`<canvas>`*
  - multimédia: *`<audio>`*, *`<video>`*
  - tabulku: *`<table>`*
  - kód: *`<pre><code>`*
  - jinou stránku: *`<iframe>`*
- ***`figcaption`*** -- popisek média uvnitř **`figure`**

---

# Formuláře: `<form>`

<pre class="code-render" default-style="" resizable="true" style="width: 40%; height: 300px; float: right; z-index: 1; margin: 2rem">
<form>
  <fieldset>
    <legend>Contact Information</legend>

    <label for="name">Name:</label>
    <input type="text" id="name" name="name">

    <label for="email">Email:</label>
    <input type="email" id="email" name="email">

    <input type="submit" value="Send">
  </fieldset>
</form>
</pre>

```html
<form>
  <fieldset>
    <legend>Contact Information</legend>

    <label for="name">Name:</label>
    <input type="text" id="name" name="name">

    <label for="email">Email:</label>
    <input type="email" id="email" name="email">

    <input type="submit" value="Send">
  </fieldset>
</form>
```

* ***`form`*** -- obsahuje libovolný flow content, ale zpravidla *formulářové ovládací prvky* a jejich *popisky*
  - `input`, `textarea`, `select` + `option`, `button`, `datalist`, `output`, `progress`, `meter`, `label`
* ***`fieldset`*** -- seskupení prvků ve formuláři, vizuálně je orámuje
* ***`legend`*** -- titulek pro skupinu, zobrazí se jako součást rámečku.

<span class="note">Principy zasílání obsahu na server v předmětu IIS -- Informační systémy</span>

---

# Horizontální oddělovač `<hr>`


```html
Udělejme za tímto tlustou čáru.
<hr>
```

```css
hr {
  height: 5px; /* určuje tloušťku. */
  border: none; /* odstraní výchozí prohlížečové okraje. */
  background-color: black; /* nebo background určuje barvu čáry. */
}
```

<pre class="code-render" default-style="
hr {
  height: 5px; /* určuje tloušťku. */
  border: none; /* odstraní výchozí prohlížečové okraje. */
  background-color: black; /* nebo background určuje barvu čáry. */
}
" resizable="true" style="height: 130px;">
Udělejme za tímto tlustou čáru.
<hr>
</pre>
