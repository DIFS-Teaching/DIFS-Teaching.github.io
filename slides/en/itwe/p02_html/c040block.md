<!-- .slide: class="section" -->

<header>
  <h1>Selected Block Elements</h1>
  <p>document structure, headings, text blocks, lists, tables, (media, forms)</p>
</header>

---

# Basic Content Structure

- **`article`** -- article, post (independently usable part of content)
- **`section`** -- chapter of an article, post, etc.
- **`aside`** -- part that only remotely relates to the main content
- **`header`** -- header of document, article, etc.
- **`footer`** -- footer
- **`main`** -- main content of the page (unique)
- **`nav`** -- part containing navigation
- **`div`** -- generic block without further meaning (for scripting, styles, etc.)

=--

<!-- .slide: class="editor" -->

# Basic Content Structure

<div data-iframe="assets/examples/html/html-structure.html"></div>

<div class="note"><a href="assets/examples/html/html-structure.html">source</a></div>

---

# Headings: h1 - h6

<pre class="code-render" default-style="" resizable="true" style="width: 50%; height: 700px; float: right; z-index: 1">
<h1>Heading level 1</h1>
<h2>Heading level 2</h2>
<h3>Heading level 3</h3>
<h4>Heading level 4</h4>
<h5>Heading level 5</h5>
<h6>Heading level 6</h6>
</pre>

```html
<h1>Heading level 1</h1>
<h2>Heading level 2</h2>
<h3>Heading level 3</h3>
<h4>Heading level 4</h4>
<h5>Heading level 5</h5>
<h6>Heading level 6</h6>
```

- elements of basic document structure usually require a heading

---

# Text Blocks

<pre class="code-render" default-style="" resizable="true" style="width: 45%; height: 500px; float: right; z-index: 1">
<p>
  This is a paragraph of text.
  Paragraphs are used
  for regular content.
</p>

<blockquote>
  “This is a quote, displayed
  as a separate block.”
</blockquote>

<address>
  Contact: John Doe
</address>
</pre>

```html
<p>
  This is a paragraph of text.
  Paragraphs are used
  for regular content.
</p>

<blockquote>
  “This is a quote, displayed
  as a separate block.”
</blockquote>

<address>
  Contact: John Doe
</address>
```

- closing tag `</p>` is not required (*not recommended*)
  - paragraph ends with the start of another block element
- only inline elements are allowed inside `p` and `address`

=--

# Text Blocks: `<details>`

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

<details open>
  <summary>Hodor</summary>
  <p>Can carry a child, a sled, and the emotional weight of his own backstory — all while saying just one word: "Hodor".</p>
</details>
```

- ***`details`***
  - can contain any HTML (text, images, lists, forms…)
  - first child must be ***`summary`*** -- changes state (attribute *`open`*)

---

# Preformatted Text

- preserves formatting using spaces and line breaks
- usually in monospaced font
- CSS property: `white-space: pre;`


```html
<pre>
  This is preformatted text.
   Preserves    line breaks  and spaces
Tags are still interpreted <b>normally</b>.
</pre>
```

<pre class="code-render" default-style="" resizable="true" style="height: 220px;">  
<pre>
  This is preformatted text.
   Preserves    line breaks  and spaces
Tags are still interpreted <b>normally</b>.
</pre>
</pre>

---

# Ordered and Unordered List

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

- *<i>unordered list</i>* ***`<ul>`*** and *<i>ordered list</i>* ***`<ol>`*** can only contain ***`<li>`*** elements
- *<i>list item</i>* ***`<li>`*** can contain any block or inline elements
  - nested lists

---

# Definition List

<pre class="code-render" default-style="" resizable="true" style="width: 40%; height: 500px; float: right; z-index: 1">
<dl>
  <dt>Ice Truck Killer</dt>
  <dd>
    Brian Moser, known for dismembering
    and arranging bodies.
  </dd>

  <dt>The Doomsday Killer</dt>
  <dd>
    Travis Marshall, murders inspired by
    the biblical Book of Revelation.
  </dd>
</dl>
</pre>

```html
<dl>
  <dt>Ice Truck Killer</dt>
  <dd>
   Brian Moser, known for dismembering
   and arranging bodies.
  </dd>

  <dt>The Doomsday Killer</dt>
  <dd>
  Travis Marshall, murders inspired by
  the biblical Book of Revelation.
  </dd>
</dl>
```

  - *<i>definition list</i>* ***`<dl>`*** can only contain ***`<dt>`*** and ***`<dd>`*** elements (in any sequence)
  - *<i>definition term</i>* ***`<dt>`*** cannot contain sections and headings
  - *<i>definition description</i>* ***`<dd>`*** can contain any block or inline elements

---

# Table

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

- table ***`<table>`*** is organized by rows ***`<tr>`*** (*<i>table row</i>*)
- rows ***`<tr>`*** contain cells ***`<td>`*** (*<i>table data</i>*) and ***`<th>`*** (*<i>table header</i>*)

---

# Table: Cell Merging

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

- ***`colspan="n"`*** -- width in columns
- ***`rowspan="n"`*** -- height in rows
- applies to ***`<td>`*** or ***`<th>`***, not **`<tr>`**

---

# Table: Style

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

/* border merging  */
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

/* border merging */
table:nth-of-type(2) {
  border-collapse: collapse;
}
```

- by default, tables have no visible borders

<span class="note">more in the CSS lecture or vertical slides...</span>

=--

# Table: Semantic Elements

```html
<table>
  <thead>
    <!-- group of rows with column headers -->
  <thead>
  <tbody>
    <!-- group of rows with main content -->
  </tbody>
  <tfoot>
    <!-- group of rows with summary or notes -->
  <tfoot>
</table>
```

- optional elements to emphasize semantics, visually not shown
  - if not specified, browser places all rows in ***`<tbody>`*** in the DOM
- ***`<tfoot>`*** can be placed before ***`<tbody>`***, browsers will display it below
  - originally (in HTML 4) this optimized table loading

=--

# Table: Column Declaration

<pre class="code-render" default-style="
table, td, th {
  border: 2px solid black;
}
" resizable="true" style="width: 40%; height: 400px; float: right; z-index: 1; margin: 2rem">
<table>
  <!-- column group -->
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
  <!-- table... -->
</table>
```

- used for bulk specification of properties for columns
  - ***`<col>`*** -- one or more columns with shared attributes
  - ***`<colgroup>`*** -- group of columns (structural)
- column definitions affect only structure, not content
- if not defined, the whole table is considered a single column group

=--

# Table: Table Caption

<pre class="code-render" default-style="
table, td, th {
  border: 2px solid black;
}

/* caption position */
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
/* caption position */
caption {
  caption-side: bottom;
}
```

- ***`<caption>`*** must be the first child of ***`<table>`***
- caption position is above the table by default
  - change using CSS property *`caption-side: top|bottom;`*

<span class="note">more in the CSS lecture</span>

---

# Media: `<figure>`

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

- ***`figure`*** -- block containing media (image, video) with caption
  - images: *`<img>`*, *`<svg>`*, *`<canvas>`*
  - multimedia: *`<audio>`*, *`<video>`*
  - table: *`<table>`*
  - code: *`<pre><code>`*
  - another page: *`<iframe>`*
- ***`figcaption`*** -- media caption inside **`figure`**

---

# Forms: `<form>`

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

* ***`form`*** -- contains any flow content, but usually *form controls* and their *labels*
  - `input`, `textarea`, `select` + `option`, `button`, `datalist`, `output`, `progress`, `meter`, `label`
* ***`fieldset`*** -- groups elements in a form, visually frames them
* ***`legend`*** -- title for the group, displayed as part of the frame.

<span class="note">Principles of sending content to the server in the [IIS](https://www.fit.vut.cz/study/course/IIS/.en) course -- Information Systems</span>

---

# Horizontal Separator `<hr>`


```html
Let's make a thick line below this.
<hr>
```

```css
hr {
  height: 5px; /* sets thickness. */
  border: none; /* removes default browser borders. */
  background-color: black; /* or background sets line color. */
}
```

<pre class="code-render" default-style="
hr {
  height: 5px; /* sets thickness. */
  border: none; /* removes default browser borders. */
  background-color: black; /* or background sets line color. */
}
" resizable="true" style="height: 130px;">
Let's make a thick line below this.
<hr>
</pre>



  
