<!-- .slide: class="section" -->
 
<header>
  <h1>Advanced CSS Features</h1>
  <p>Filters, Transformations, Transitions, Animations</p>
</header>

---

# Motivation

- modern CSS evolves through ***independent modules and levels*** rather than big version numbers like CSS3 or CSS4.
- **[W3C current work](https://www.w3.org/Style/CSS/current-work)**

<br>

- **vendor prefixes**
  - used to enable experimental or draft features before standardization
  - `-moz-` Firefox
  - `-ms-` IE
  - `-webkit-` Chrome, Safari
  - `-o-` Opera (obsolete)

---

# New Features: Container Queries

```css
<div class="post">
  <div class="card">
    <h2>Card title</h2>
    <p>Card content</p>
  </div>
</div>
```

- create a **containment context**, use [Container Query Length Units](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/length#container_query_length_units)

```css
.post {
  container-type: inline-size; /* containment context */
}

@container (width > 700px) {
  .card h2 {
    font-size: max(1.5em, 1.23em + 2cqi);
    /* cqi - 1% of a query container's inline size */
  }
}
```

<span class="note">[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Containment/Container_queries)</span>

---

# New Features: Subgrid

```html
<div class="grid">
  <div class="item">
    <div class="subitem"></div>
  </div>
</div>
```

<pre class="code-render" default-style="

* {
  box-sizing: border-box;
}

.grid {
  display: grid;
  grid-template-columns: repeat(9, 1fr);
  border: 4px solid red;
  gap: .5rem;
  padding: 4px 0;
  
}

.item {
  display: grid;
  grid-column: 2 / 7;
  grid-row: 1/2;
  grid-template-columns: subgrid;
  border: 4px solid blue;
  padding: 4px 0;
}

.subitem {
  grid-column: 3 / 6;
  grid-row: 1/2;
  border: 4px solid green;
  height: 200px;
}

.subitem2 {
  grid-row: 1/2;
  background-color: lightgray;
  padding: 12px 8px;
}


" resizable="true" style="width: 45%; height: 500px; float: right; z-index: 1; position: relative">

<div class="grid">
  <div class="subitem2" style="grid-column: 1">1</div>
  <div class="subitem2" style="grid-column: 2">2</div>
  <div class="subitem2" style="grid-column: 3">3</div>
  <div class="subitem2" style="grid-column: 4">4</div>
  <div class="subitem2" style="grid-column: 5">5</div>
  <div class="subitem2" style="grid-column: 6">6</div>
  <div class="subitem2" style="grid-column: 7">7</div>
  <div class="subitem2" style="grid-column: 8">8</div>
  <div class="subitem2" style="grid-column: 9">9</div>
  <div class="item">
    <div class="subitem"></div>
  </div>
</div>

</pre>

```css
.grid { /* red */
  display: grid;
  grid-template-columns: repeat(9, 1fr);
}

.item { /* blue */
  display: grid;
  grid-column: 2 / 7;
  grid-template-columns: subgrid;
}

.subitem { /* green */
  grid-column: 3 / 6;
}
```

<span class="note">[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Grid_layout/Subgrid)</span>

---

# New Features...

- [CSS Nesting](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Nesting)
- [`:has()`](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/:has) pseudo-class
- [Style Queries](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Containment/Container_size_and_style_queries)
- [`:scope`](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/:scope) / [`@scope`](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/@scope)
- Cascade Layers ([`@layer`](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/@layer))
- [`@property`](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/@property) rule
- [`color()`](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/color_value/color) -- support for HWB/LAB/LCH
- Color mixing and blending -- e.g., [`color-mix()`](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/color_value/color-mix)
- New viewport [units](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics/Values_and_units) (`svh`, `lvh`, `dvh`)
- [CSS Math](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math) & trigonometry -- e.g., `sin()`, `cos()`
- ...

---

# filter

- enables simple visual effects directly in CSS without graphics editing tools.

<pre class="code-render" default-style="

img {
  margin: 20px;
  filter:
    grayscale(80%)
    sepia(.8)
    contrast(120%)
    brightness(110%)
    drop-shadow(0px 5px 10px black);
}

img:hover {
  filter: none;
}

" resizable="true" style="width: 45%; height: 500px; float: right; z-index: 1; position: relative">
<img src='https://www.fit.vut.cz/study/course/ITW/public/assets/cat-fall-small.jpg' alt='Cat'>
</pre>

```css
img {
  filter:
    grayscale(40%)
    sepia(.8)
    contrast(120%)
    brightness(110%)
    drop-shadow(0px 5px 10px black);
}

img:hover {
  filter: none;
}
```

<span class="note">[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/filter)</span>

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/animations/filter.html"></div>

<div class="note"><a href="assets/examples/animations/filter.html">source</a></div>

---

# transform

- lets you rotate, scale, translate, and skew elements in 2D and 3D space.

<pre class="code-render" default-style="

img {
  margin: 20px;
  transform: rotate(15deg) scale(.5) translateX(50%) skewY(5deg);
}

img:hover {
  transform: none;
}

" resizable="true" style="width: 45%; height: 500px; float: right; z-index: 1; position: relative">
<img src='https://www.fit.vut.cz/study/course/ITW/public/assets/cat-fall-small.jpg' alt='Cat'>
</pre>

```css
img {
  transform:
    rotate(15deg)
    scale(.5)
    translateX(50%)
    skewY(5deg);
}

img:hover {
  transform: none;
}
```

<span class="note">[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/transform)</span>

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/animations/transform.html"></div>

<div class="note"><a href="assets/examples/animations/transform.html">source</a></div>

---

# transition

- lets you smoothly animate changes to CSS properties over a specified duration.
- `transition: property duration timing-function delay;`

<pre class="code-render" default-style="

img {
  margin: 20px;
  filter: grayscale(80%) sepia(.8) contrast(120%) brightness(110%) drop-shadow(0px 5px 10px black);
  transform: rotate(15deg) scale(.5) translateX(50%) skewY(5deg);
  transition: all .5s ease;
}

img:hover {
  transform: none;
  filter: none;
}

" resizable="true" style="width: 45%; height: 500px; float: right; z-index: 1; position: relative">
<img src='https://www.fit.vut.cz/study/course/ITW/public/assets/cat-fall-small.jpg' alt='Cat'>
</pre>

```css
img {
  filter: ... ;
  transform: ... ;
  transition: all .5s ease;
}

img:hover {
  filter: none;
  transform: none;
}
```

<span class="note">[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/transition)</span>

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/animations/transition.html"></div>

<div class="note"><a href="assets/examples/animations/transition.html">source</a></div>

---

# animation, @keyframes

- let you create repeated or timed changes to element properties ***without JavaScript***.
- `animation: name duration timing-function delay iteration-count direction;`

<pre class="code-render" default-style="

@keyframes bounce {
  0%, 100% {
    transform: translateY(0);
  }
  20% {
    transform: translateX(200px); 
    width: 200px;
  }
  50% {
    transform: translate(300px, 100px) rotate(360deg);
    width: 400px;
  }
}

img {
  width: 200px;
  margin: 50px 20px;
  animation: bounce 5s infinite;
}

" resizable="true" style="width: 45%; height: 600px; float: right; z-index: 1; position: relative">
<img src='https://www.fit.vut.cz/study/course/ITW/public/assets/cat-fall-small.jpg' alt='Cat'>
</pre>

```css
@keyframes bounce {
  0%, 100% {
    transform: translateY(0);
  }
  20% {
    transform: translateX(200px); 
    width: 200px;
  }
  50% {
    transform: translate(300px, 100px)
               rotate(360deg);
    width: 400px;
  }
}
img {
  width: 200px;
  animation: bounce 5s infinite;
}
```

<span class="note">[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/animation)</span>

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/animations/animation.html"></div>

<div class="note"><a href="assets/examples/animations/animation.html">source</a></div>

