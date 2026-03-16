# Table style

  - We can change the style of
    - The whole table - `<table>`
    - Rows - `<tr>`
    - Cells - `<td>`, `<th>`
    - Columns - `<col>`, `<colgroup>`
    - Header, footer, body - `<thead>`, `<tfoot>`, `<tbody>`
    - Caption - `<caption>`

---

# Table caption

<pre class="code-render" default-style="
table {
    border-collapse: collapse;
    border: 1px solid #aaa;
    margin-bottom: 1.5em;
}
td, th { padding: 0.2em 0.8em; border: 1px solid #ccc; }
caption { font-weight: bold; font-style: italic; }
.top caption { caption-side: top; }
.bottom caption { caption-side: bottom; }
" resizable="false" style="height:15em" >
<table class="top">
    <caption>Tab 1. Caption on the top</caption>
    <tr><th>Name</th><th>Surname</th></tr>
    <tr><td>John</td><td>Wayne</td></tr>
    <tr><td>Albert</td><td>Einstein</td></tr>
</table>
<table class="bottom">
    <caption>Tab 2. Caption in the bottom</caption>
    <tr><th>Name</th><th>Surname</th></tr>
    <tr><td>John</td><td>Wayne</td></tr>
    <tr><td>Albert</td><td>Einstein</td></tr>
</table>
</pre>

```css
.top caption { caption-side: top; }
.bottom caption { caption-side: bottom; }
```

---

# Borders in a table

  - Borders can be set separately for the cells or the whole table
  - Special properties:
    - `border-collapse: separate | collapse` \- cell border merging
    - `border-spacing: 5px` \- cell border spacing
    - `empty-cells: show | hide` \- whether to diplay or not the empty cells

---

# Border Examples

<pre class="code-render" default-style="
* { font-family: sans-serif }
table { margin-bottom: 0.8em; font-size: 0.85em; }
td, th { padding: 0.15em 0.5em; }
.t1 { border-collapse: separate; border: 1px solid #999; }
.t1 td, .t1 th { border: 1px solid #999; }
.t2 { border-collapse: collapse; border: 1px solid #999; }
.t2 td, .t2 th { border: 1px solid #999; }
.t3 { border-collapse: collapse; }
.t3 tr { border-top: 1px solid #555; }
.t4 { border: 1px solid #555; border-collapse: collapse; }
.t4 th { border: 1px solid #555; }
.t4 td { border: none; border-left: 1px solid #555; }
" resizable="true" style="height: 420px; width: 90%; margin: auto">
<p><code>border-collapse: separate</code></p>
<table class="t1">
    <tr><th>Name</th><th>Surname</th></tr>
    <tr><td>John</td><td>Wayne</td></tr>
    <tr><td>Albert</td><td>Einstein</td></tr>
</table>
<p><code>border-collapse: collapse</code></p>
<table class="t2">
    <tr><th>Name</th><th>Surname</th></tr>
    <tr><td>John</td><td>Wayne</td></tr>
    <tr><td>Albert</td><td>Einstein</td></tr>
</table>
<p><code>tr { border-top: 1px solid }</code> (rows only)</p>
<table class="t3">
    <tr><th>Name</th><th>Surname</th></tr>
    <tr><td>John</td><td>Wayne</td></tr>
    <tr><td>Albert</td><td>Einstein</td></tr>
</table>
<p><code>table + th border, td left border only</code></p>
<table class="t4">
    <tr><th>Name</th><th>Surname</th></tr>
    <tr><td>John</td><td>Wayne</td></tr>
    <tr><td>Albert</td><td>Einstein</td></tr>
</table>
</pre>

```css
/* separate borders (default) */
table { border-collapse: separate; }
/* merged borders */
table { border-collapse: collapse; }
/* horizontal lines only */
table tr { border-top: 1px solid; }
/* full outer + left cell borders */
table { border: 1px solid; }
table th { border: 1px solid; }
table td { border: none; border-left: 1px solid; }
```

---

# Lists: Bullet and Numbering Types

<div class="col textbox">
    <strong>Unordered (<code>ul</code>)</strong>
    <ul>
        <li style="list-style-type: disc">disc (default)</li>
        <li style="list-style-type: circle">circle</li>
        <li style="list-style-type: square">square</li>
        <li style="list-style-type: none">none</li>
    </ul>
</div>
<div class="col textbox">
    <strong>Ordered (<code>ol</code>)</strong>
    <ol>
        <li style="list-style-type: decimal">decimal</li>
        <li style="list-style-type: lower-roman">lower-roman</li>
        <li style="list-style-type: upper-roman">upper-roman</li>
        <li style="list-style-type: lower-alpha">lower-alpha</li>
        <li style="list-style-type: upper-alpha">upper-alpha</li>
        <li style="list-style-type: none">none</li>
    </ol>
</div>

  - The `list-style-type` property — applied to the `<li>` element

```css
ul li { list-style-type: square; }
ol li { list-style-type: lower-roman; }
```

---

# Bullet position

  - The `list-style-position` property

<pre class="code-render" default-style="
.outside { list-style-position: outside; background: #eef; }
.inside { list-style-position: inside; background: #efe; }
ul { width: 18em; margin: 0.3em auto; padding-left: 2em; }
" resizable="false" style="height: 15em">
<p><code>list-style-position: outside</code> (default):</p>
<ul class="outside">
    <li>First item in longer text in longer text in longer text in longer text...</li>
</ul>
<p><code>list-style-position: inside</code>:</p>
<ul class="inside">
    <li>First item in longer text in longer text in longer text in longer text...</li>
</ul>
</pre>

---

# Mouse cursor

  - The `cursor` property allows to change the mouse cursor look when placed over the particular element on the page.

<pre class="code-render" default-style="" resizable="true" >
The cursor over this
<span style="cursor: crosshair">word</span>
has a different shape.
</pre>

```html
The cursor over this
<span style="cursor: crosshair">word</span>
has a different shape.
```

---

# Cursor types

<table style="width: 20em">
<tr><td style="cursor: auto">auto</td><td style="cursor: crosshair">crosshair</td><td style="cursor: default">default</td></tr>
<tr><td style="cursor: hand">hand</td><td style="cursor: pointer">pointer</td><td style="cursor: move">move</td></tr>
<tr><td style="cursor: text">text</td><td style="cursor: wait">wait</td><td style="cursor: help">help</td></tr>
</table>
<table style="width: 20em">
<tr><td style="cursor: nw-resize">nw-resize</td><td style="cursor: n-resize">n-resize</td><td style="cursor: ne-resize">ne-resize</td></tr>
<tr><td style="cursor: w-resize">w-resize</td><td></td><td style="cursor: e-resize">e-resize</td></tr>
<tr><td style="cursor: sw-resize">sw-resize</td><td style="cursor: s-resize">s-resize</td><td style="cursor: se-resize">se-resize</td></tr>
</table>

---

# Pseudo Elements and Classes

  - Abstract class for denoting special elements or their state
  - They define the look of various parts
    - **Pseudo classes** : in different states
      - E.g. links visited, not visited, focused, etc.
      - Specificity as for classes
      - Denoted by „:"
    - **Pseudo elements** : different parts of elements
      - First element, first letter, before, after, ...
      - Specificity as for elements
      - Denoted by „::"
    - `p::first-letter { font-size: 20px; }`

---

# Pseudo Classes: Link Style

  - Static
    - Not visited link:
`a:link { color: green; }`
    - Visited link:
`a:visited { color: red; }`
  - Dynamic
    - Mouse moved over:
`a:hover { ... }`
    - Link activation:
`a:active { ... }`
    - Keyboar focus:
`a:focus { ... }`

---

# Typical Link Style

  - Highlighted by color, underlines on moving mouse over
  - It gets highlighed when activated, gets darker when visited

<pre class="code-render" default-style="
a { color: #aaf; text-decoration: none; }
a:link { }
a:visited { color: #339; }
a:hover { text-decoration: underline; }
a:active { text-decoration: underline; color: red; }
" resizable="true">
Example: <a href="#">Sample link</a>.
</pre>

```css
a { color: #aaf; text-decoration: none; }
a:link { }
a:visited { color: #339; }
a:hover { text-decoration: underline; }
a:active { text-decoration: underline; color: red; }
```

---

# Pseudo Class :first-child

  - The first child element of its parent element

<pre class="code-render" default-style="
.menu li { color: green; }
.menu li:first-child { color: blue; }
" resizable="true">
<ul class="menu">
    <li>Blue item</li>
    <li>Green item</li>
    <li>Green item</li>
</ul>
</pre>

```html
<ul class="menu">
    <li>Blue item</li>
    <li>Green item</li>
    <li>Green item</li>
</ul>
```

```css
.menu li { color: green; }
.menu li:first-child { color: blue; }
```

  - Similarly `last-child`, and much more...

---

# Pseudo Elements: Firtst Letters and Lines

  - Element `::first-line`
    - Denotes the first line of an arbitrary element
    - E.g. `p::first-line` \- first line of a paragraph
    - Depends on the window width, font size, ...
  - Element `::first-letter`
    - Denotes first letter of an element
    - E.g. `p::first-letter` \- first letter of a paragraph

---

# Example 1

<pre class="code-render" default-style="
p { text-transform: none; }
p::first-line { text-transform: uppercase; }
" resizable="true" style="width: 50%">
<p>First line of this paragraph will be in capital letters. Any text follows. Any text follows. Any text follows.</p>
</pre>

```css
p { text-transform: none; }
p::first-line { text-transform: uppercase; }
```

```html
<p>First line of this line will
be in capital letters. Any text follows. Any text follows.
Any text follows.</p>
```

---

# Example 2

<pre class="code-render" default-style="
p::first-letter {
    font-size: 200%;
    font-weight: bold;
    float: left;
}
" resizable="true" style="width: 50%">
<p>First letter will be large and floated by the remaining text. Other text as normal. Other text as normal. Other text as normal.</p>
</pre>

```css
p::first-letter {
    font-size: 200%;
    font-weight: bold;
    float: left;
}
```

```html
<p>First letter will be large and floated
by the remaining text. Other text as normal. Other text as normal.
Other text as normal.</p>
```

---

# Generated content

  - Allows to generate a text that is not present in the document
  - Pseudo-elements `::before` and `::after`
  - The `content:` property

<pre class="code-render" default-style="
div.remark:before {
    content: 'Remark: ';
    font-weight: bold;
}
" resizable="true">
<div class="remark">This rule doesn't always apply.</div>
</pre>

```css
div.remark::before {
    content: "Remark: ";
    font-weight: bold;
}
```

```html
<div class="remark">This rule doesn't always apply.</div>
```
