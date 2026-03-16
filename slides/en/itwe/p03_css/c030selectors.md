<!-- .slide: class="section" -->

<header>
  <h1>Selectors</h1>
  <p>simple, structured, pseudo-classes, pseudo-selectors</p>
</header>

---

# Selector

- an operation that returns a ***set of elements***
  - properties are applied to the selected elements

- there are ***different types of selectors***
  - *simple* -- e.g. `p`, `.class`, `#id`, `[attribute]`
  - *structured* -- e.g. `div > p`, `a + b`
  - *pseudo-classes* -- `:hover`
  - *pseudo-elements* -- `::before`

- each selector has a certain ***specificity*** (`id` > `class` > `element`), which determines which style takes precedence
  - will be covered in the next lecture

=--

<!-- .slide: class="editor" -->

# Overview of CSS Selectors

<div data-iframe="assets/examples/selectors/selectors.html"></div>

<div class="note"><a href="assets/examples/selectors/selectors.html">source</a></div>

---

# Universal Selector: <code>*</code>

- applies to ***all elements in the document***

<pre class="code-render" default-style="
:not(.code-tag) {
  border: 4px solid green;
  background-color: #00FF0011;
}
" resizable="true" style="width: 50%; height: 700px; float: right; z-index: 1" tags="true">
&lt;body&gt;

<h1>&lt;h1&gt;ITW&lt;/h1&gt;</h1>

<h2>&lt;h2&gt;About&lt;/h2&gt;</h2>

<p>&lt;p&gt;Hello! You shall <i>&lt;i&gt;not&lt;/i&gt;</i> pass!.&lt;/p&gt;</p>

<h2>&lt;h2&gt;Lectures&lt;/h2&gt;</h2>

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

# Type Selector: <code>tag</code>

- applies to all elements ***of the given name***

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

<h2>&lt;h2&gt;About&lt;/h2&gt;</h2>

<p>&lt;p&gt;Hello! You shall <i>&lt;i&gt;not&lt;/i&gt;</i> pass!.&lt;/p&gt;</p>

<h2>&lt;h2&gt;Lectures&lt;/h2&gt;</h2>

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

# Class Selector: <code>.class</code>

- applies to all elements ***of the given class***
  - multiple elements can share a class, and one element can have multiple classes

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

<h2>&lt;h2&gt;About&lt;/h2&gt;</h2>

<p>&lt;p&gt;Hello! You shall <i class="red box">&lt;i class="red box"&gt;not&lt;/i&gt;</i> pass!.&lt;/p&gt;</p>

<h2 class="box red">&lt;h2 class="box red"&gt;Lectures&lt;/h2&gt;</h2>

<p class="box">&lt;p class="box"&gt;...&lt;/p&gt;</p>
</pre>

```css
.box {
  border: 4px solid blue;
  background-color: lightblue;
}

h2.box {
  /* overrides .box */
  border: 4px solid green;
  background-color: lightgreen;
}

/* same as .red */
*.red {
  color: red;
}
```

<span class="note">[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Type_selectors)</span>

---

# ID Selector: <code>#id</code>

- applies to the unique element ***with the given identifier***
  - if there are ***incorrectly*** multiple, it applies to all occurrences

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

<h2>&lt;h2&gt;About&lt;/h2&gt;</h2>

<p>&lt;p&gt;Hello! You shall <i id="unique">&lt;i id="unique"&gt;not&lt;/i&gt;</i> pass!.&lt;/p&gt;</p>

<h2>&lt;h2&gt;Lectures&lt;/h2&gt;</h2>

<p>&lt;p&gt;...&lt;/p&gt;</p>
</pre>

```css
#unique {
  border: 4px solid blue;
  background-color: lightblue;
}

/* generally doesn't make much sense,
   since according to the
   HTML specification
   it should be a unique
   element in the document */
i#unique {
  color: red;
}
```

<span class="note">[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/ID_selectors)</span>

---

# Attribute Selector: <code>[attribute]</code>

- applies to all elements whose attributes match the condition

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

<h2 title="design">&lt;h2 title="design"&gt;About&lt;/h2&gt;</h2>

<p>&lt;p&gt;Hello! You shall <i title="design">&lt;i title="design"&gt;not&lt;/i&gt;</i> pass!.&lt;/p&gt;</p>

<h2 title="Web design">&lt;h2 title="Web design"&gt;Lectures&lt;/h2&gt;</h2>

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

- <em>*=</em> substring, *^=* prefix, *$=* suffix
- *~=* substring separated by whitespace
- *|=* value starts with the string or the string followed by a hyphen

<span class="note">[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors)</span>

---

# Structured Selectors

- compound selector: ***<code>s1 op s2</code>***, where op is the following operator

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
/* descendants */
article p {
  color: red;
}

/* direct children */
article > p {
  border: 4px solid blue;
}

/* following siblings */
div ~ p {
  background-color: lightblue;
}

/* immediately following sibling */
div + p {
  font-style: italic;
  font-weight: bold;
}
```

---

# Grouping

- multiple rules with the same properties can be grouped into one rule

```css
h1 {
  color: red;
  font-weight: bold;
}

section h2 {
  color: red;
}
```

- grouping for the property *`color: red`*

```css
h1, section h2 {
  color: red;
}

h1 {
  font-weight: bold;
}
```

---

# Pseudo-classes

- special selectors starting with *`:`*, targeting the *state* of an element, its *position*, or *logical context*:

<pre class="code-render" default-style="
:root {
  border: 4px solid red;
}

h2:hover {
  color: blue;
}

p:nth-of-type(1) {
  border: 4px solid blue;
}


h2, p, div {
  margin: 0.5rem 0;
}
" resizable="true" style="width: 50%; height: 600px; float: right; z-index: 1" tags="true">
&lt;article&gt;
<article>

<h2>&nbsp;&nbsp;&lt;h2&gt;About&lt;/h2&gt;</h2>

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
p:nth-of-type(1) {
  border: 4px solid blue;
}

h2:hover {
  color: blue;
}
```

- more in vertical slides or next lectures...

=--

# Pseudo-classes

- **types:**

  - ***stateful*** (user interaction)
    - `:hover`, `:active`, `:focus`, `:target`, ...
  - ***form states***
    - `:enabled`, `:checked`, `:valid`, `:required`, ...
  - ***structural*** (position in DOM)
    - `:root`, `:first-child`, `:nth-child(n)`, `:first-of-type`, ...
  - ***logical***
    - `:not`, `:is`, `:where`, `:has`, ...
  - ***others*** (language, links, and other special...)
    - `:lang`, `:dir`, `:link`, `:visited`, ...

=--

# Pseudo-classes: stateful

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
<a href="#about">&lt;a href="#about"&gt;About&lt;/a&gt;</a>
<br>

<article id="about">
&lt;article id="about"&gt;

<h2 id="about">&lt;h2&gt;About&lt;/h2&gt;</h2>

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
/* mouse hover */
article *:hover {
  color: blue;
}

/* mouse click and hold */
article *:active {
  color: red;
}

/* active via TAB key */
article *:focus {
  border: 6px solid green;
}

/* clicking a link
   referring to an element */
body *:target {
  border: 4px solid orange;
}
```

=--

# Pseudo-classes: form states

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

=--

# Pseudo-classes: structural

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

<h2>&nbsp;&nbsp;&lt;h2&gt;About&lt;/h2&gt;</h2>

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

- ***node order in parent:***
  - `:first-child`, `:last-child`, `:only-child`, `:nth-child(n)`, `:nth-last-child(n)`
- ***type order in parent:***
  - `:first-of-type`, `:last-of-type`, `:only-of-type`,<br> `:nth-of-type(n)`, `:nth-last-of-type(n)`

=--

# Pseudo-classes: logical

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

<h2>&nbsp;&nbsp;&lt;h2&gt;About&lt;/h2&gt;</h2>

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
/* all elements containing h2 */
*:has(> h2) {
  border: 4px solid blue;
}

/* all elements except article,
   containing p as a direct child */
:not(article):has(> p) {
  border: 4px solid green;
}

/* all h2 and p elements,
   that are direct children of article */
article > :is(h2, p) {
  color: red;
}

/* all elements except p and div,
   that are direct children of article or div */
:where(article, div) > :not(:is(p, div)) {
  border: 4px solid orange;
}
```

<span class="note">priority and differences between `:is` and `:where` in the next lecture</span>

=--

# Pseudo-classes: other specific...

- *`:lang()`* -- language-based selection (attribute `lang`)
- *`:dir(rtl)`* -- elements with right-to-left text direction (e.g. Arabic, Hebrew)
- *`:link`* -- unvisited links
- *`:visited`* -- links the user has visited
- *`:any-link`* -- all links (`:link` and `:visited`)
- and many more...

<br>

- more in **[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_selectors#selectors)**...

---

# Pseudo-elements

- part of CSS selectors (not a selector itself) starting with *`::`*, allowing you to target a specific part of an element, *even if there is no separate tag for it in HTML*:

<pre class="code-render" default-style="

/* First line of text will be bold and blue */
p::first-line {
  font-weight: bold;
  color: blue;
}

/* First letter will be huge and red */
p::first-letter {
  font-size: 3em;
  color: red;
  float: left;
  margin-right: 5px;
}

/* Text selected by the user will have yellow background and black text */
p::selection {
  background: yellow;
  color: black;
}

" resizable="true" style="width: 40%; height: 400px; float: right; z-index: 1; margin-left: 1rem;" tags="true">

&lt;p&gt;<p>You shall not pass!. One ring to rule them all, one ring to find them, One ring to bring them all and in the darkness bind them.</p>&lt;/p&gt;

</pre>

```css
p::first-line {
  font-weight: bold;
  color: blue;
}

p::first-letter {
  font-size: 3em;
  color: red;
  float: left;
  margin-right: 5px;
}

p::selection {
  background: yellow;
  color: black;
}
```

- more in vertical slides or next lectures...

=--

# Pseudo-elements

- **types:**
  - ***text*** (targeting part of text)
    - `::first-line`, `::first-letter`, `::selection`, ...
  - ***input and form*** (specific for `<input>`, `<textarea>`, and forms)
    - `::placeholder`, `::file-selector-button`, `::cue`, ...
  - ***content*** (for adding or manipulating content)
    - `::before`, `::after`
  - ***other special***
    - [`::marker`](https://developer.mozilla.org/en-US/docs/Web/CSS/::marker) -- list item marker styling `<li>`
    - [`::cue`](https://developer.mozilla.org/en-US/docs/Web/CSS/::cue) -- subtitle styling in `<track>` for `<video>`
    - ...

=--

# Pseudo-elements: text

<pre class="code-render" default-style="

/* First line of text will be bold and blue */
p::first-line {
  font-weight: bold;
  color: blue;
}

/* First letter will be huge and red */
p::first-letter {
  font-size: 3em;
  color: red;
  float: left;
  margin-right: 5px;
}

/* Text selected by the user will have yellow background and black text */
p::selection {
  background: yellow;
  color: black;
}

" resizable="true" style="width: 40%; height: 400px; float: right; z-index: 1; margin-left: 1rem;" tags="true">

&lt;p&gt;<p>You shall not pass!. One ring to rule them all, one ring to find them, One ring to bring them all and in the darkness bind them.</p>&lt;/p&gt;

</pre>

```css
/* First line of text will be bold and blue */
p::first-line {
  font-weight: bold;
  color: blue;
}

/* First letter will be huge and red */
p::first-letter {
  font-size: 3em;
  color: red;
  float: left;
  margin-right: 5px;
}

/* Text selected by the user will
   have yellow background and black text */
p::selection {
  background: yellow;
  color: black;
}
```

=--

# Pseudo-elements: input and form

<pre class="code-render" default-style="
input {
  font-size: 1rem;
}

input::placeholder {
  color: SandyBrown;
  font-style: italic;
}

/* File input button – style the button */
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

<h2>&lt;h2&gt;Project 1&lt;/h2&gt;</h2>

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

/* style the button */
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

=--

# Pseudo-elements: content

- possibility to add new elements to the DOM

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

- part of the element (first or last child)
- the rule must always contain the ***`content`*** property

