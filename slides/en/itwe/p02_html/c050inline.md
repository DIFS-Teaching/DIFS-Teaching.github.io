<!-- .slide: class="section" -->

<header>
  <h1>Selected Inline Elements</h1>
  <p>text highlighting, links</p>
</header>

---

# Text Highlighting: Semantic Distinction

<pre class="code-render" default-style="
table {
  width: 100%;
}

td, th {
  padding: .5rem;
}

th {
  background-color: #eaeaea;
  text-align: left;
}

tr:nth-child(2n+1) td {
  background-color: #eaeaea;
}

.first {
  width: 400px;
}

" resizable="true" style="height: 710px; margin: 2rem">
<table>
  <colgroup>
    <col class="first">
    <col>
  </colgroup>
  <tr>
    <td>&lt;em&gt;</td>
    <td><em>emphasized text</em> -- italic with meaning for screen readers</td>
  </tr>
  <tr>
    <td>&lt;strong&gt;</td>
    <td><strong>important text</strong> -- bold, has meaning for screen readers</td>
  </tr>
  <tr>
    <td>&lt;b&gt;</td>
    <td><b>bold text</b> -- older, only visual boldness</td>
  </tr>
  <tr>
    <td>&lt;i&gt;</td>
    <td><i>italic</i> -- older, only visual italics</td>
  </tr>
  <tr>
    <td>&lt;u&gt;</td>
    <td><u>underlined text</u> -- visual underline</td>
  </tr>
  <tr>
    <td>&lt;mark&gt;</td>
    <td><mark>highlighted text</mark> -- yellow background</td>
  </tr>
  <tr>
    <td>&lt;small&gt;</td>
    <td><small>smaller text</small> -- smaller font</td>
  </tr>
  <tr>
    <td>&lt;s&gt;</td>
    <td><s>strikethrough text</s> -- obsolete or invalid</td>
  </tr>
  <tr>
    <td>&lt;abbr title=""&gt;</td>
    <td><abbr title="World Health Organization">WHO</abbr> -- abbreviation with explanation</td>
  </tr>
</table>
</pre>

---

# Text Highlighting: Formulas, Code, Quotes

<pre class="code-render" default-style="
table {
  width: 100%;
}

td, th {
  padding: .5rem;
}

th {
  background-color: #eaeaea;
  text-align: left;
}

tr:nth-child(2n+1) td {
  background-color: #eaeaea;
}

.first {
  width: 400px;
}

" resizable="true" style="height: 780px; margin: 2rem">
<table>
  <colgroup>
  <col class="first">
    <col>
  </colgroup>
  <tr>
    <td>&lt;var&gt;</td>
    <td><var>x</var> -- variable in code or formula</td>
  </tr>
  <tr>
    <td>&lt;sub&gt;</td>
    <td>H<sub>2</sub>O -- subscript</td>
  </tr>
  <tr>
    <td>&lt;sup&gt;</td>
    <td>10<sup>2</sup> -- superscript</td>
  </tr>
  <tr>
    <td>&lt;code&gt;</td>
    <td><code>console.log("Code")</code> -- monospace font for code</td>
  </tr>
  <tr>
    <td>&lt;dfn&gt;</td>
    <td><dfn>HTML</dfn> -- new term</td>
  </tr>
  <tr>
    <td>&lt;kbd&gt;</td>
    <td><kbd>Ctrl</kbd> + <kbd>C</kbd> -- keyboard input</td>
  </tr>
  <tr>
    <td>&lt;q&gt;</td>
    <td><q>Short quote</q> -- inserted quotation marks</td>
  </tr>
  <tr>
    <td>&lt;cite&gt;</td>
    <td><cite>Author of work</cite> -- name of source/work</td>
  </tr>
  <tr>
    <td>&lt;time&gt;</td>
    <td><time datetime="09:00">9 AM</time> – <time datetime="17:00">5 PM</time></td>
  </tr>
  <tr>
    <td>&lt;data value=""&gt;</td>
    <td><data value="CZ">Czech Republic</data></td>
  </tr>
</table>
</pre>

---

# Links

```html
<a href="https://en.wikipedia.org/wiki/Tyrion_Lannister">
  Tyrion Lannister
</a>,
<a href="https://en.wikipedia.org/wiki/Tyrion_Lannister#Character"
   title="Wikipedia" target="_blank">
  Character of Tyrion Lannister
</a>
```

<pre class="code-render" default-style="" resizable="true" style="height: 100px;">
<a href="https://en.wikipedia.org/wiki/Tyrion_Lannister">
  Tyrion Lannister
</a>,
<a href="https://en.wikipedia.org/wiki/Tyrion_Lannister#Character"
   title="Wikipedia" target="_blank" rel="noopener noreferrer">
  Character of Tyrion Lannister
</a>
</pre>

<br>

- `target="_blank"` -- opens the link in a new window or tab.
- `title` -- short description of the link (shown on hover).
- [`rel="noopener noreferrer"`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/rel) -- security recommendation for links with target="_blank".

---

# Links: URL

- **to another server**
  - *`href="http://www.vutbr.cz/"`*
  - *`href="http://www.vutbr.cz/doc/info.html"`*
- **To the same server**
  - Absolute *`href="/doc/info.html"`*
  - Relative to current document location
  - *`href="next.html"`*
  - *`href="obsah/clanek.html"`*
  - *`href="../index.html"`*

---

# Links: Anchors

```html
<a href="#Character">Character of Tyrion Lannister</a>
...
<p id="Character">
  Drinks wine like it’s water, talks like every word costs gold,
  and somehow survives when everyone else doesn’t.
</p>
```

<br>

- *`"#Character"`* -- current document
- *`"wiki/Tyrion_Lannister#Character"`* -- another document
- *`"https://en.wikipedia.org/wiki/Tyrion_Lannister#Character"`* -- another server

---

# Line Breaks

```html
Doctor Who<br>
1 TARDIS Lane<br>
Llanfairpwllg<wbr>wyngyllgogerych<wbr>wyrndrobwllllantysiliog<wbr>ogogoch<br>
Anglesey, Wales<br>
UK
```

<pre class="code-render" default-style="" resizable="true" style="height: 260px;">
Doctor Who<br>
1 TARDIS Lane<br>
Llanfairpwllg<wbr>wyngyllgogerych<wbr>wyrndrobwllllantysiliog<wbr>ogogoch<br>
Anglesey, Wales<br>
UK
</pre>

<br>

- ***`<br>`*** -- hard (forced) line break
- ***`<wbr>`*** -- optional line break (Word Break Opportunity)
  - does not break unless needed (e.g. for narrow window)

