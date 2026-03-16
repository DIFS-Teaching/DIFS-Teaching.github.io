<!-- .slide: class="section" -->

<header>
	<h1>Vybrané řádkové elementy</h1>
	<p>zvýraznění textu, odkazy</p>
</header>

---

# Zvýraznění textu: významové odlišení textu

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
    <td><em>zdůrazněný text</em> -- kurzíva s významem pro čtečky</td>
  </tr>
  <tr>
    <td>&lt;strong&gt;</td>
    <td><strong>důležitý text</strong> -- tučný, má význam pro čtečky</td>
  </tr>
  <tr>
    <td>&lt;b&gt;</td>
    <td><b>tučný text</b> -- starší, pouze vizuální tučnost</td>
  </tr>
  <tr>
    <td>&lt;i&gt;</td>
    <td><i>kurzíva</i> -- starší, pouze vizuální kurzíva</td>
  </tr>
  <tr>
    <td>&lt;u&gt;</td>
    <td><u>podtržený text</u> -- vizuální podtržení</td>
  </tr>
  <tr>
    <td>&lt;mark&gt;</td>
    <td><mark>zvýrazněný text</mark> -- žluté podbarvení</td>
  </tr>
  <tr>
    <td>&lt;small&gt;</td>
    <td><small>menší text</small> -- drobnější písmo</td>
  </tr>
  <tr>
    <td>&lt;s&gt;</td>
    <td><s>přeškrtnutý text</s> -- zastaralé nebo neplatné</td>
  </tr>
  <tr>
    <td>&lt;abbr title=""&gt;</td>
    <td><abbr title="World Health Organization">WHO</abbr> -- zkratka s vysvětlením</td>
  </tr>
</table>
</pre>

---

# Zvýraznění textu: vzorce, programy, citace

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
    <td><var>x</var> -- proměnná v programu, vzorci</td>
  </tr>
  <tr>
    <td>&lt;sub&gt;</td>
    <td>H<sub>2</sub>O -- dolní index</td>
  </tr>
  <tr>
    <td>&lt;sup&gt;</td>
    <td>10<sup>2</sup> -- horní index</td>
  </tr>
  <tr>
    <td>&lt;code&gt;</td>
    <td><code>console.log("Kód")</code> -- kódové písmo</td>
  </tr>
  <tr>
    <td>&lt;dfn&gt;</td>
    <td><dfn>HTML</dfn> -- nový termín</td>
  </tr>
  <tr>
    <td>&lt;kbd&gt;</td>
    <td><kbd>Ctrl</kbd> + <kbd>C</kbd> -- vstup z klávesnice</td>
  </tr>
  <tr>
    <td>&lt;q&gt;</td>
    <td><q>Krátká citace</q> -- vložené uvozovky</td>
  </tr>
  <tr>
    <td>&lt;cite&gt;</td>
    <td><cite>Autor díla</cite> -- název zdroje/díla</td>
  </tr>
  <tr>
    <td>&lt;time&gt;</td>
    <td><time datetime="09:00">9 AM</time> – <time datetime="17:00">5 PM</time></td>
  </tr>
  <tr>
    <td>&lt;data value=""&gt;</td>
    <td><data value="CZ">Česká republika</data></td>
  </tr>
</table>
</pre>

---

# Odkazy

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

- `target="_blank"` -- otevře odkaz v novém okně nebo panelu.
- `title` -- krátký popis odkazu (zobrazí se při najetí myší).
- [`rel="noopener noreferrer"`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/rel) -- bezpečnostní doporučení pro odkazy s target="_blank".

---

# Odkazy: URL

- **na jiný server**
  - *`href="http://www.vutbr.cz/"`*
  - *`href="http://www.vutbr.cz/doc/info.html"`*
- **Na stejný server**
  - Absolutní *`href="/doc/info.html"`*
  - Relativní k umístění souč. dokumentu
    - *`href="next.html"`*
    - *`href="obsah/clanek.html"`*
    - *`href="../index.html"`*

---

# Odkazy: kotvy

```html
<a href="#Character">Character of Tyrion Lannister</a>
...
<p id="Character">
  Drinks wine like it’s water, talks like every word costs gold,
  and somehow survives when everyone else doesn’t.
</p>
```

<br>

- *`"#Character"`* -- současný dokument
- *`"wiki/Tyrion_Lannister#Character"`* -- jiný dokument
- *`"https://en.wikipedia.org/wiki/Tyrion_Lannister#Character"`* -- jiný server

---

# Zalomení řádku

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

- ***`<br>`*** -- pevné (vynucené) zalomení řádku
- ***`<wbr>`*** -- volitelné zalomení řádku (Word Break Opportunity)
  - neudělá žádné zalomení, dokud to není potřeba (např. kvůli úzkému oknu)


