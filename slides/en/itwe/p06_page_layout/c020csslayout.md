# CSS Layout

  - Visual blocks are created mostly using the sectioning HTML elements 
    - Semantic elements `<header>`, `<footer>`, `<article>`, ...
    - The `<div>` element for remaining parts
    - The `id` and `class` attributes
  - The positions of the elements are defined by CSS 
    - Width and height
    - Margins
    - Floating blocks
    - Positioning (absolute or relative)
    - Flex and grid layout

---

# Page width

  - Fixed width $\times$ flexible
  - Design aspects
    - Wide range of browsing devices 
      - Desktop even 2560px, mobile phone 320px
    - It's inconvenient to read long text lines 
      - Use narrow lines
      - Greater font
      - More columns
  - Currently, we prefer flexible width

---

# Page setup

- HTML `<div>` container

```html
<body>
    <div id="page">
        ... page content ....
    </div>
</body>
```

<div class="col">

- Flexible width

```css
body {
    margin: 0; padding: 1em;
}
#page {
    width: 80%;
    margin: auto;
    padding: 1em;
}
```

</div>

<div class="col">

- Fixed width

```css
body {
    margin: 0; padding: 1em;
}
#page {
    width: 1000px;
    margin: auto;
    padding: 1em;
}
```
</div>

=--

<!-- .slide: class="editor" -->

# Page Width -- Example

<div data-iframe="assets/examples/page_w_rel.html"></div>

<span class="note"><a href="assets/examples/page_w_rel.html">source:flexible</a></span>
<span class="note"><a href="assets/examples/page_w_abs.html">source:fixed</a></span>

---

# Positioning the elements side-by-side

  - With tables: for small local areas 
    - Fixed small parts of the page, form fields, ...
    - Easy to set up
  - Absolute positioning
  - Floating objects
  - Special `display:` values (e.g. inline-block)
  - Flexbox
  - Grid layout

---

# Absolute positioning

  - Left element has absolute position
  - Right element has a right margin

<div class="col">

```html
<div id="left">Left</div>
<div id="right">Right</div>
```

```css
#left {
    width: 5em;
    position: absolute;
    left: 0; top: 0;
}
#right {
    margin-left: 5em;
}
```

</div>

<pre class="code-render" class="col" default-style="
body {
  padding: 0;
  position: relative;
}
#left {
    width: 5em;
    position: absolute;
    left: 0; top: 0;
}
#right {
    margin-left: 5em;
}
#left {
    width: 5em;
    height: 5em;
    background-color: green;
    font-size: 2em;
    color: white;
    text-align: center;
    line-height: 5em;
}
#right {
    width: 5em;
    height: 5em;
    background-color: blue;
    font-size: 2em;
    color: white;
    text-align: center;
    line-height: 5em;
}
" resizable="false" style="padding: 0; height: 10em">

<div id="left">Left</div>
<div id="right">Right</div>

</pre>


---

# Absolute positioning -- Disadvantages

- How to determine the vertical position?
- Absolutely positioned element may overlap with other content

<div class="col">

```html
<p>Preceding paragraph</p>
<div id="left">Left</div>
<div id="right">Right</div>
<p>Following paragraph</p>
```

```css
#left {
    width: 5em;
    position: absolute;
    left: 0; top: 0.5em;
}
#right {
    margin-left: 5em;
}
```

</div>

<pre class="code-render" class="col" default-style="
body {
  padding: 0;
  position: relative;
}
#left {
    width: 5em;
    position: absolute;
    left: 0; top: 0.5em;
}
#right {
    margin-left: 5em;
}
#left {
    width: 5em;
    height: 5em;
    background-color: green;
    font-size: 2em;
    color: white;
    text-align: center;
    line-height: 5em;
}
#right {
    width: 5em;
    height: 5em;
    background-color: blue;
    font-size: 2em;
    color: white;
    text-align: center;
    line-height: 5em;
}
" resizable="false" style="padding: 0; height: 15em">

<p>Preceding paragraph</p>
<div id="left">Left</div>
<div id="right">Right</div>
<p>Following paragraph</p>

</pre>

---

# Absolute positioning -- Container

- Absolute positioning within a parent element (container) with _position: relative_

<div class="col">

```html
<p>Preceding paragraph</p>
<div class="columns">
  <div id="left">Left</div>
  <div id="right">Right</div>
</div>
<p>Following paragraph</p>
```

```css
.columns {
    position: relative;
}
#left {
    width: 5em;
    position: absolute;
    left: 0; top: 0em;
}
#right {
    margin-left: 5em;
}
```

</div>

<pre class="code-render" class="col" default-style="
body {
  padding: 0;
  position: relative;
}
.columns {
    position: relative;
}
#left {
    width: 5em;
    position: absolute;
    left: 0; top: 0em;
}
#right {
    margin-left: 5em;
}
#left {
    width: 5em;
    height: 5em;
    background-color: green;
    font-size: 2em;
    color: white;
    text-align: center;
    line-height: 5em;
}
#right {
    width: 5em;
    height: 5em;
    background-color: blue;
    font-size: 2em;
    color: white;
    text-align: center;
    line-height: 5em;
}
" resizable="false" style="padding: 0; height: 15em">

<p>Preceding paragraph</p>
<div class="columns">
  <div id="left">Left</div>
  <div id="right">Right</div>
</div>
<p>Following paragraph</p>

</pre>

What if we need more than two columns?

---

# Floating Blocks

- All columns have `float: left`

<div class="col">

```html
<p>Preceding paragraph</p>
<div id="left" class="col">Left</div>
<div id="right" class="col">Right</div>
<p>Following paragraph</p>
```

```css
.col {
    width: 5em;
    float: left;
}
```

</div>

<pre class="code-render" class="col" default-style="
body {
  padding: 0;
  position: relative;
}
.col {
    width: 5em;
    float: left;
}
#left {
    width: 5em;
    height: 5em;
    background-color: green;
    font-size: 2em;
    color: white;
    text-align: center;
    line-height: 5em;
}
#right {
    width: 5em;
    height: 5em;
    background-color: blue;
    font-size: 2em;
    color: white;
    text-align: center;
    line-height: 5em;
}
" resizable="false" style="padding: 0; height: 15em">

<p>Preceding paragraph</p>
<div id="left" class="col">Left</div>
<div id="right" class="col">Right</div>
<p>Following paragraph</p>

</pre>

---

# Floating Blocks with `clear`

- Use `clear: left` or `both` for the following paragraph

<div class="col">

```html
<p>Preceding paragraph</p>
<div id="left" class="col">Left</div>
<div id="right" class="col">Right</div>
<p class="clear">Following paragraph</p>
```

```css
.col {
    width: 5em;
    float: left;
}
.clear {
    clear: both;
}
```

</div>

<pre class="code-render" class="col" default-style="
body {
  padding: 0;
  position: relative;
}
.col {
    width: 5em;
    float: left;
}
.clear {
    clear: both;
}
#left {
    width: 5em;
    height: 5em;
    background-color: green;
    font-size: 2em;
    color: white;
    text-align: center;
    line-height: 5em;
}
#right {
    width: 5em;
    height: 5em;
    background-color: blue;
    font-size: 2em;
    color: white;
    text-align: center;
    line-height: 5em;
}
" resizable="false" style="padding: 0; height: 15em">

<p>Preceding paragraph</p>
<div id="left" class="col">Left</div>
<div id="right" class="col">Right</div>
<p class="clear">Following paragraph</p>

</pre>

---

<!-- .slide: data-transition="slide-in fade-out" -->

# Floating Blocks -- Container

- The enclosing block `.columns` remains empty

<div class="col">

```html
<p>Preceding paragraph</p>
<div class="columns">
  <div id="left" class="col">Left</div>
  <div id="right" class="col">Right</div>
</div>
<p>Following paragraph</p>
```

```css
.col {
    width: 5em;
    float: left;
}
.columns {
    clear: both;
    border: 5px solid black;
}
```

</div>

<pre class="code-render" class="col" default-style="
body {
  padding: 0;
  position: relative;
}
.col {
    width: 5em;
    float: left;
}
.columns {
    clear: both;
    border: 5px solid black;
}
#left {
    width: 5em;
    height: 5em;
    background-color: green;
    font-size: 2em;
    color: white;
    text-align: center;
    line-height: 5em;
}
#right {
    width: 5em;
    height: 5em;
    background-color: blue;
    font-size: 2em;
    color: white;
    text-align: center;
    line-height: 5em;
}
" resizable="false" style="padding: 0; height: 15em">

<p>Preceding paragraph</p>
<div class="columns">
  <div id="left" class="col">Left</div>
  <div id="right" class="col">Right</div>
</div>
<p>Following paragraph</p>

</pre>

---

<!-- .slide: data-transition="fade-in slide-out" -->

# Floating Blocks -- Container with overflow

- With `overflow: hidden`, the block `.columns` encloses all floating blocks

<div class="col">

```html
<p>Preceding paragraph</p>
<div class="columns">
  <div id="left" class="col">Left</div>
  <div id="right" class="col">Right</div>
</div>
<p>Following paragraph</p>
```

```css
.col {
    width: 5em;
    float: left;
}
.columns {
    clear: both;
    border: 5px solid black;
    overflow: hidden;
}
```

</div>

<pre class="code-render" class="col" default-style="
body {
  padding: 0;
  position: relative;
}
.col {
    width: 5em;
    float: left;
}
.columns {
    clear: both;
    border: 5px solid black;
    overflow: hidden;
}
#left {
    width: 5em;
    height: 5em;
    background-color: green;
    font-size: 2em;
    color: white;
    text-align: center;
    line-height: 5em;
}
#right {
    width: 5em;
    height: 5em;
    background-color: blue;
    font-size: 2em;
    color: white;
    text-align: center;
    line-height: 5em;
}
" resizable="false" style="padding: 0; height: 15em">

<p>Preceding paragraph</p>
<div class="columns">
  <div id="left" class="col">Left</div>
  <div id="right" class="col">Right</div>
</div>
<p>Following paragraph</p>

</pre>

---

<!-- .slide: class="editor" -->

# Multiple columns

<div data-iframe="assets/examples/col_floats.html"></div>

<span class="note"><a href="assets/examples/col_floats.html">source</a></span>

---

# Special `display` Property Values

- Inline block `display: inline-block`
  - Blocks positioned as inline elements
- Table cells `display: table-cell`
  - They create an _anonymous table_
  - Similarly `table-row`, `table`, `inline-table`

=--

<!-- .slide: class="editor" -->

# Special `display` Property Values -- Examples

<div data-iframe="assets/examples/col_display.html"></div>

<span class="note"><a href="assets/examples/col_display.html">source</a></span>
