<!-- .slide: class="section" -->
 
<header>
  <h1>Grid System: Flexbox</h1>
</header>

---

# Flexbox

- a tool for arranging elements in one dimension (row/column)
  - covered in lecture [CSS -- Page Layout](https://gitshow.net/gh/DIFS-Teaching/slides@main/en/itwe/p06_page_layout)

<br>

- the layout consists of:

<br>

<ol style="display: flex; justify-content: space-around; width: 100%;">
  <li>
  
  ***containers*** (<i>flex container</i>)
  
  </li>
  <li>
  
  ***container items*** (<i>flex items</i>)
  
  </li>
</ol>

<div style="text-align: center;">
  <img src="assets/flexbox.png" alt="Flexbox" style="width: 80%; margin-left: 100px;">
</div>

<span class="note"><a href="https://css-tricks.com/snippets/css/a-guide-to-flexbox/">Image source</a></span>

---

# 1. Flex Container: Row

- a parent element that contains other elements we want to position within the container

```css
.row {
  display: flex;

  flex-direction: row; /* setting the main axis - row orientation
              not necessary to set, default value */
  
  flex-wrap: wrap; /* items will wrap if they overflow */

  align-items: stretch; /* alignment of items on the cross axis
               row items will occupy the full height of the row */
}
```

---

# 2. Flex Container Items: Columns

```css
[class*="col-"] {
  flex-basis: 100%; /* base size */
  flex-grow: 1; /* width growth will be even for all columns */
  flex-shrink: 1; /* width reduction will be even for all columns */
}

@media only screen and (min-width: 768px) {
  .col-sm-1 { flex-basis: 25%; }
  .col-sm-2 { flex-basis: 50%; }
  .col-sm-3 { flex-basis: 75%; }
  .col-sm-4 { flex-basis: 100%; }
}

/* etc... */
```

---

# All Together

<pre class="code-render" default-style="

* {
  box-sizing: border-box;
}

body {
  background-color: lightyellow;
}

.row {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: start;
  align-items: stretch;
  border: 4px solid blue;
  max-width: 1400px;
  margin: auto;
  background: white;
}

[class*='col-'] {
  flex-basis: 100%;
  flex-grow: 1;
  flex-shrink: 1;
  border: 2px solid red;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1rem;
  padding-top: 2rem;
  position: relative;
}

[class*='col-']::after {
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
}

h2 {
  margin: 0;
}

article, nav {
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
  .col-md-1 { flex-basis: 25%; } /* 1/4 */
  .col-md-2 { flex-basis: 50%; } /* 2/4 */
  .col-md-3 { flex-basis: 75%; } /* 3/4 */
  .col-md-4 { flex-basis: 100%; } /* 4/4 */
  .col-md-1::after { content: 'col: 1/4' }
  .col-md-2::after { content: 'col: 2/4' }
  .col-md-3::after { content: 'col: 3/4' }
  .col-md-4::after { content: 'col: 4/4' }
}

@media only screen and (min-width: 1200px) {
  .col-lg-1 { flex-basis: 25%; } /* 1/4 */
  .col-lg-2 { flex-basis: 50%; } /* 2/4 */
  .col-lg-3 { flex-basis: 75%; } /* 3/4 */
  .col-lg-4 { flex-basis: 100%; } /* 4/4 */
  .col-lg-1::after { content: 'col: 1/4' }
  .col-lg-2::after { content: 'col: 2/4' }
  .col-lg-3::after { content: 'col: 3/4' }
  .col-lg-4::after { content: 'col: 4/4' }
}

" resizable="true" style="height: 800px;">

body
<header id="content" class="row">
  <h2 class="col-lg-4 col-md-4">
    Web Development
  </h2>
</header>
<main id="content" class="row">
  <nav class="col-lg-1 col-md-2">
  <ul>
    <li>About the Course</li>
    <li>Schedule</li>
    <li>Lectures</li>
    <li>Exercises</li>
    <li>Project</li>
  </ul>
  </nav>
  <article class="col-lg-3 col-md-2">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies lectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit, faucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </article>
</main>

</pre>

<span class="note">💡 test different example widths</span>

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/responsive/flex.html"></div>

<div class="note"><a href="assets/examples/responsive/flex.html">source</a></div>

---

# Summary

- especially useful when positioning elements within one dimension (e.g., in a row)
  - compared to floats, it offers additional properties (e.g., *`align-items`*, *`gap`* ...)

<br>

- responsiveness can be achieved in alternative ways:
  - using the *`wrap`* property combined with *`min-width`* -- items will wrap when the page width decreases
  - defining *`flex-grow`* and *`flex-shrink`* properties for each element individually + combining with Media Queries
  - ...

<br>

- ***disadvantages***
  - still necessary to wrap row elements in a separate container
  - the Grid system uses utility classes in HTML (*`row`*, *`col-`*)
  - solution: ***CSS Grid***
