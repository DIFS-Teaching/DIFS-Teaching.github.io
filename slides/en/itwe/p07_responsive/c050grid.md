<!-- .slide: class="section" -->
 
<header>
  <h1>Grid System: CSS Grid</h1>
</header>

---

# CSS Grid

- a tool for arranging elements in two dimensions (rows + columns)
  - covered in lecture [CSS -- Page Layout](https://gitshow.net/gh/DIFS-Teaching/slides@main/en/itwe/p06_page_layout)
- the most advanced tool for arranging elements in CSS so far
- allows easy definition of a Grid system without modifying the HTML document

<div class="img-right box" style="width: 700px; text-align: center;">
  <img src="assets/grid.svg" alt="CSS Grid" style="width: 100%;">
</div>

<br>

- the layout consists of:
  1. ***container*** (<i>grid container</i>)
   - contains a *grid* (<i>grid</i>) made up of *cells* (<i>cells</i>)
   - groups of cells form *tracks* or *areas* (<i>tracks</i>, <i>areas</i>),<br> which map to *container items* (<i>grid items</i>)
  2. ***container items*** (<i>grid items</i>)
   - elements (direct children) of the container

<span class="note"><a href="https://css-tricks.com/snippets/css/a-guide-to-flexbox/">Image source</a></span>

---

# 1. Grid Container: Layout

- the parent element that forms the grid
- we choose a layout strategy using ***`grid-template-areas`***

```css
.container {
  display: grid;

  grid-template-columns: repeat(4, 1fr); /* 4-column layout */

  grid-template-areas: "header header header header"
             "sidebar content content content";
             /* custom naming of areas - creating the layout itself */
}
```

<pre class="code-render" default-style="

* {
  box-sizing: border-box;
}

.container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  text-align: center;
  align-items: center;
  justify-content: center;
}

.container > div {
  height: 100px;
  border: 2px solid black;
  display: flex;
  align-items: center;
  justify-content: center;
}

.header {
  color: blue;
}

.sidebar {
  color: green;
}

.content {
  color: red;
}

" resizable="true" style="height: 280px;">

<div class="container">
  <div class="header">header</div>
  <div class="header">header</div>
  <div class="header">header</div>
  <div class="header">header</div>
  <div class="sidebar">sidebar</div>
  <div class="content">content</div>
  <div class="content">content</div>
  <div class="content">content</div>
</div>

</pre>

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/responsive/grid1.html"></div>

<div class="note"><a href="assets/examples/responsive/grid1.html">source</a></div>

---

# 2. Grid Container Items

<div style="float: right; width: 800px; z-index: 1; position: relative;">

```html
<div class="container">
  <header>header</header>
  <nav>nav</nav>
  <article>article</article>
</div>
```

</div>

```css
header {
  grid-area: header;
}

nav {
  grid-area: sidebar;
}

article {
  grid-area: content;
}
```

<pre class="code-render" default-style="

* {
  box-sizing: border-box;
}

.container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-areas: 'header header header header'
             'sidebar content content content';
  text-align: center;
  align-items: center;
  justify-content: center;
}

.container > * {
  height: 100px;
  border: 2px solid lightgray;
  color: lightgray;
  display: flex;
  align-items: center;
  justify-content: center;
}

.container > div:nth-child(1) { grid-area: 1 / 1 / 2 / 2; }
.container > div:nth-child(2) { grid-area: 1 / 2 / 2 / 3; }
.container > div:nth-child(3) { grid-area: 1 / 3 / 2 / 4; }
.container > div:nth-child(4) { grid-area: 1 / 4 / 2 / 5; }
.container > div:nth-child(5) { grid-area: 2 / 1 / 3 / 2; }
.container > div:nth-child(6) { grid-area: 2 / 2 / 3 / 3; }
.container > div:nth-child(7) { grid-area: 2 / 3 / 3 / 4; }
.container > div:nth-child(8) { grid-area: 2 / 4 / 3 / 5; }

.container > header {
  grid-area: header;
  color: blue;
  border: 4px solid blue;
  background-color: #0000FF22;
  justify-content: left;
  padding: .2rem;
}

.container > nav {
  grid-area: sidebar;
  color: green;
  border: 4px solid green;
  background-color: #00FF0022;
  justify-content: left;
  padding: .2rem;
}

.container > article {
  grid-area: content;
  color: red;
  border: 4px solid red;
  background-color: #FF000022;
  justify-content: left;
  padding: .2rem;
}

" resizable="true" style="height: 280px;">

<div class="container">
  <div class="header">header</div>
  <div class="header">header</div>
  <div class="header">header</div>
  <div class="header">header</div>
  <div class="sidebar">sidebar</div>
  <div class="content">content</div>
  <div class="content">content</div>
  <div class="content">content</div>

  <header>header</header>
  <nav>nav</nav>
  <article>article</article>
</div>

</pre>

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/responsive/grid2.html"></div>

<div class="note"><a href="assets/examples/responsive/grid2.html">source</a></div>

---

# 3. Responsive Grid

```css
.container {
  display: grid;
  grid-template-columns: 1fr;
  grid-template-areas: "header"
             "sidebar"
             "content";
}
@media only screen and (min-width: 768px) {
  .container {
  grid-template-columns: repeat(2, 1fr);
  grid-template-areas: "header header"
             "sidebar content";
  }
}
@media only screen and (min-width: 1200px) {
  .container {
  grid-template-columns: repeat(4, 1fr);
  grid-template-areas: "header header header header"
             "sidebar content content content";
  }
}
```

---

# 3. Responsive Grid

<pre class="code-render" default-style="

* {
  box-sizing: border-box;
}

body {
  background-color: lightyellow;
}

.container {
  display: grid;
  grid-template-columns: 1fr;
  grid-template-areas: 'header'
             'sidebar'
             'content';
  justify-content: start;
  align-items: stretch;
  border: 4px solid blue;
  max-width: 1400px;
  margin: auto;
  background: white;
}

.container > * {
  border: 2px solid red;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1rem;
  padding-top: 2rem;
  position: relative;
}

.container > *::after {
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
  grid-area: header;
}

h2 {
  margin: 0;
}

nav {
  grid-area: sidebar;
  background-color: bisque;
}

article {
  grid-area: content;
  background-color: bisque;
}

nav ul {
  align-self: start;
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
  .container {
  grid-template-columns: repeat(2, 1fr);
  grid-template-areas: 'header header'
             'sidebar content';
  }
  .container > header::after { content: 'col: 2/2' }
  .container > nav::after { content: 'col: 1/2' }
  .container > article::after { content: 'col: 1/2' }
}

@media only screen and (min-width: 1200px) {
  .container {
  grid-template-columns: repeat(4, 1fr);
  grid-template-areas: 'header header header header'
             'sidebar content content content';
  }
  .container > header::after { content: 'col: 4/4' }
  .container > nav::after { content: 'col: 1/4' }
  .container > article::after { content: 'col: 3/4' }
}

" resizable="true" style="height: 800px;">

body
<div class="container">
  <header>
  <h2>
    Web Development
  </h2>
  </header>
  <nav>
  <ul>
    <li>About the Course</li>
    <li>Schedule</li>
    <li>Lectures</li>
    <li>Exercises</li>
    <li>Project</li>
  </ul>
  </nav>
  <article>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies lectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit, faucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </article>
</div>

</pre>

<span class="note">💡 test different example widths</span>

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/responsive/grid3.html"></div>

<div class="note"><a href="assets/examples/responsive/grid3.html">source</a></div>

---

# Responsive Grid Without Media Queries

```css
.container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr) minmax(300px, 1fr));
  gap: .5rem;
}
```

<pre class="code-render" default-style="

* {
  box-sizing: border-box;
}

.container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr) minmax(300px, 1fr));
  gap: .5rem;
}

.container > div {
  border: 2px solid red;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: green;
}

.container > *:nth-child(odd) {
   color: black;
}

.container > *:nth-child(even) {
   color: gray;
}

p {
  font-size: 14px;
  text-align: justify;
  margin: 0;
  background-color: white;
}

" resizable="true" style="height: 500px;">

<div class="container">
  <div>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies lectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit, faucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
  <div>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies lectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit, faucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
  <div>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies lectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit, faucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
  <div>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies lectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit, faucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
</div>

</pre>

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/responsive/grid4.html"></div>

<div class="note"><a href="assets/examples/responsive/grid4.html">source</a></div>

---

# Summary

- CSS Grid provides advanced options for arranging elements
  - compared to Flexbox, it allows 2D arrangement (rows + columns) -- complete layout definition
  - no need to define a container for each row
  - no need to use utility classes in the HTML document (*`row`*, *`col-`*)
