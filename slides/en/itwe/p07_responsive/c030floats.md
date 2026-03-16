<!-- .slide: class="section" -->
 
<header>
  <h1>Grid System: Floats</h1>
</header>

---

# 1. Rows

- blocks will be positioned into columns on rows -- class ***.row***

<br>

- necessary to address ***issues with floating elements:***
  - *clear: both* -- breaking floating (float) blocks after each row:
  ```css
  .row::after {
      content: "";
      clear: both;
  }
  ```
  - *overflow: hidden* -- some columns in a row may have a smaller height than the resulting row height
(columns of the next row could overlap the previous row):
  ```css
  .row {
      overflow: hidden;
  }
  ```

---

# 2. Columns

- elements will be organized into columns within a row:

<br>

- necessary to define classes for columns of different widths:
  ```css
  [class*="col-"] { float: left; }

  .col-1 { width: 25%; } /* 1/4 */
  .col-2 { width: 50%; } /* 2/4 */
  .col-3 { width: 75%; } /* 3/4 */
  .col-4 { width: 100%; } /* 4/4 */
  ```
  - the ***`float`*** property causes elements to float and align side by side 
  - the ***`width`*** property determines how much space a column will relatively occupy in a row
  - the number of columns can be chosen to best suit the specific problem
  - a *12-column layout* is often used (easily divisible)

---

# 2. Columns: HTML

- classes will be assigned to elements in the HTML document based on the desired layout:

```html
<div id="content" class="row">
  <div id="sidebar" class="col-1">
    <!-- 1/4 -->
  </div>
  <div id="article" class="col-3">
    <!-- 3/4 -->
  </div>
</div>
```

<pre class="code-render" default-style="
.row {
  overflow: hidden;
  border: 4px solid blue;
}

.row::after {
  content: '';
  clear: both;
}

[class*='col-'] {
  float: left;
  height: 200px;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
}

#sidebar {
  background-color: lightblue;
}

#article {
  background-color: lightpink;
}

.col-1 { width: 25%; } /* 1/4 */
.col-2 { width: 50%; } /* 2/4 */
.col-3 { width: 75%; } /* 3/4 */
.col-4 { width: 100%; } /* 4/4 */

" resizable="true" style="height: 300px;">

<div id="content" class="row">
  <div id="sidebar" class="col-1">
    sidebar<br>1/4
  </div>
  <div id="article" class="col-3">
    article<br>3/4
  </div>
</div>

</pre>

<span class="note">💡 Test different example widths</span>

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/responsive/floats1.html"></div>

<div class="note"><a href="assets/examples/responsive/floats1.html">source</a></div>

---

# 3. Breakpoints

- use ***Media Queries*** for breakpoints for different browser window (viewport) widths
  - e.g., [Bootstrap breakpoints](https://getbootstrap.com/docs/5.3/layout/breakpoints/), ...

```css
/* Small devices – default display */
[class*="col-"] { float: left; width: 100%; }

/* Medium devices (tablet) */
@media only screen and (min-width: 768px) {
  .col-md-1 { width: 25%; }
  .col-md-2 { width: 50%; }
  ...
}

/* Large devices (PC) */
@media only screen and (min-width: 1200px) {
  .col-lg-1 { width: 25%; }
  .col-md-2 { width: 50%; }
  ...
}
```

---

# 3. Breakpoints: HTML

- classes will be assigned to elements in the HTML document based on the desired layout<br> for different width groups:

```html
<div id="content" class="row">
  <div id="sidebar" class="col-md-2 col-lg-1">
  </div>
  <div id="article" class="col-md-2 col-lg-3">
  </div>
</div>
```

<pre class="code-render" default-style="

.row {
  overflow: hidden;
  border: 4px solid blue;
}

.row::after {
  content: '';
  clear: both;
}

[class*='col-'] {
  float: left;
  width: 100%;
  height: 200px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
}

#sidebar {
  background-color: lightblue;
}

#article {
  background-color: lightpink;
}

[class*='col-']::after {
  content: '100%'
}

@media only screen and (min-width: 768px) {
  .col-md-1 { width: 25%; } /* 1/4 */
  .col-md-2 { width: 50%; } /* 2/4 */
  .col-md-3 { width: 75%; } /* 3/4 */
  .col-md-4 { width: 100%; } /* 4/4 */
  .col-md-1::after { content: '1/4' }
  .col-md-2::after { content: '2/4' }
  .col-md-3::after { content: '3/4' }
  .col-md-4::after { content: '4/4' }
}

@media only screen and (min-width: 1200px) {
  .col-lg-1 { width: 25%; } /* 1/4 */
  .col-lg-2 { width: 50%; } /* 2/4 */
  .col-lg-3 { width: 75%; } /* 3/4 */
  .col-lg-4 { width: 100%; } /* 4/4 */
  .col-lg-1::after { content: '1/4' }
  .col-lg-2::after { content: '2/4' }
  .col-lg-3::after { content: '3/4' }
  .col-lg-4::after { content: '4/4' }
}

" resizable="true" style="height: 300px;">

<div id="content" class="row">
  <div id="sidebar" class="col-lg-1 col-md-2">
    sidebar
  </div>
  <div id="article" class="col-lg-3 col-md-2">
    article
  </div>
</div>

</pre>

<span class="note">💡 Test different example widths</span>

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/responsive/floats2.html"></div>

<div class="note"><a href="assets/examples/responsive/floats2.html">source</a></div>

---

# 4. Border and Padding

- often, we want to set some ***`padding`*** or ***`border`*** for blocks positioned into columns

<pre class="code-render" default-style="

.row {
  overflow: hidden;
  border: 4px solid blue;
}

.row::after {
  content: ' ';
  clear: both;
}

[class*='col-'] {
  float: left;
  border: 0px solid red;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: green;
}

.row > *:nth-child(odd) {
   color: black;
}

.row > *:nth-child(even) {
   color: gray;
}

p {
  font-size: 14px;
  text-align: justify;
  margin: 0;
  background-color: white;
}

#form {
  margin-bottom: .5rem;
}

input {
  font-size: 24px;
}

.col-1 { width: 25%; } /* 1/4 */
.col-2 { width: 50%; } /* 2/4 */
.col-3 { width: 75%; } /* 3/4 */
.col-4 { width: 100%; } /* 4/4 */

" resizable="true" style="height: 600px;">

<div id="form">
  border: <input id="border-width" type="number" min="0" value="0">
  padding: <input id="padding" type="number" min="0" value="0">
</div>

<div id="content" class="row">
  <div class="col-1">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
  <div class="col-1">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
  <div class="col-1">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
  <div class="col-1">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
</div>

<script>
  function setListener(type) {
  let elem = document.getElementById(type);
  if(elem) {
    elem.addEventListener("change", (e) => {
    let cols = document.querySelectorAll("[class*='col-']");
    for(let i = 0; i < cols.length; i++) {
      cols[i].style[type] = elem.value + "px";
    }
    });
  }
  }

  setListener("border-width");
  setListener("padding");
</script>

</pre>

<div style="text-align: center; margin-top: 4rem">

**Actual box width** = <span style="color: lightgray">`margin`</span> + <span style="color: red">`border`</span> + <span style="color: green">`padding`</span> + `width`

</div>

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/responsive/floats3.html"></div>

<div class="note"><a href="assets/examples/responsive/floats3.html">source</a></div>

---

# 4. Border and Padding: box-sizing

- the ***`box-sizing`*** property allows you to modify the box model equation

<br>

- value ***`content-box`*** (default):

<div class="box" style="text-align: center; margin-top: 4rem; padding: 1rem;">

**Actual box width** = <span style="color: lightgray">`margin`</span> + <span style="color: red">`border`</span> + <span style="color: green">`padding`</span> + `width`

</div>

<br>

- value ***`border-box`***:

<div class="box" style="text-align: center; margin-top: 4rem; padding: 1rem;">

  **Actual box width** = <span style="color: lightgray">`margin`</span> + `width`<br>
  `width` = <span style="color: red">`border`</span> + <span style="color: green">`padding`</span> + *actual content width* (calculated automatically)

</div>

<br>

- column margins should be 0 (this property is not set)

---

# 4. Border and Padding: box-sizing

- set all elements' ***`box-sizing`*** to ***`border-box`***:

```css
* {
  box-sizing: border-box;
}
```

- *`padding`* and *`border`* will be *subtracted* from the actual box width:

<pre class="code-render" default-style="

* {
  box-sizing: border-box;
}

.row {
  overflow: hidden;
  border: 4px solid blue;
}

.row::after {
  content: ' ';
  clear: both;
}

[class*='col-'] {
  float: left;
  border: 0px solid red;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: green;
}

.row > *:nth-child(odd) {
   color: black;
}

.row > *:nth-child(even) {
   color: gray;
}

p {
  font-size: 14px;
  text-align: justify;
  margin: 0;
  background-color: white;
}

#form {
  margin-bottom: .5rem;
}

input {
  font-size: 24px;
}

.col-1 { width: 25%; } /* 1/4 */
.col-2 { width: 50%; } /* 2/4 */
.col-3 { width: 75%; } /* 3/4 */
.col-4 { width: 100%; } /* 4/4 */

" resizable="true" style="height: 400px;">

<div id="form">
  border: <input id="border-width" type="number" min="0" value="0">
  padding: <input id="padding" type="number" min="0" value="0">
</div>

<div id="content" class="row">
  <div class="col-1">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
  <div class="col-1">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
  <div class="col-1">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
  <div class="col-1">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
</div>

<script>
  function setListener(type) {
    let elem = document.getElementById(type);
    if(elem) {
      elem.addEventListener("change", (e) => {
        let cols = document.querySelectorAll("[class*='col-']");
        for(let i = 0; i < cols.length; i++) {
          cols[i].style[type] = elem.value + "px";
        }
      });
    }
  }

  setListener("border-width");
  setListener("padding");
</script>

</pre>

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/responsive/floats4.html"></div>

<div class="note"><a href="assets/examples/responsive/floats4.html">source</a></div>

---

# 5. Margin

- often it is appropriate to set some ***margins*** -- we set them for the row ***`.row`*** or for a container that wraps all rows

```css
.row { max-width: 1400px; margin: auto; }
```

<pre class="code-render" default-style="

* {
  box-sizing: border-box;
}

body {
  background-color: lightyellow;
}

.row {
  overflow: hidden;
  border: 4px solid blue;
  max-width: 1400px;
  margin: auto;
  background: white;
}

.row::after {
  content: ' ';
  clear: both;
}

[class*='col-'] {
  float: left;
  border: 2px solid red;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1rem;
}

header {
  text-align: center;
}

h2 {
  margin: 0;
}

p {
  font-size: 20px;
  text-align: justify;
  margin: 0;
  background-color: white;
}

ul {
  margin: 0;
  font-size: 30px;
}

.col-1 { width: 25%; } /* 1/4 */
.col-2 { width: 50%; } /* 2/4 */
.col-3 { width: 75%; } /* 3/4 */
.col-4 { width: 100%; } /* 4/4 */

" resizable="true" style="height: 550px;">

body
<header id="content" class="row">
  <h2 class="col-4">
    Web Page Development
  </h2>
</header>
<main id="content" class="row">
  <nav class="col-1">
    <ul>
      <li>About the Subject</li>
      <li>Schedule</li>
      <li>Lectures</li>
      <li>Exercises</li>
      <li>Project</li>
    </ul>
  </nav>
  <article class="col-3">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit, aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </article>
</main>

</pre>

<span class="note">💡 Test different example widths</span>

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/responsive/floats5.html"></div>

<div class="note"><a href="assets/examples/responsive/floats5.html">source</a></div>

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
  overflow: hidden;
  border: 4px solid blue;
  max-width: 1400px;
  margin: auto;
  background: white;
}

.row::after {
  content: ' ';
  clear: both;
}

[class*='col-'] {
  float: left;
  width: 100%;
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
  .col-md-1 { width: 25%; } /* 1/4 */
  .col-md-2 { width: 50%; } /* 2/4 */
  .col-md-3 { width: 75%; } /* 3/4 */
  .col-md-4 { width: 100%; } /* 4/4 */
  .col-md-1::after { content: 'col: 1/4' }
  .col-md-2::after { content: 'col: 2/4' }
  .col-md-3::after { content: 'col: 3/4' }
  .col-md-4::after { content: 'col: 4/4' }
}

@media only screen and (min-width: 1200px) {
  .col-lg-1 { width: 25%; } /* 1/4 */
  .col-lg-2 { width: 50%; } /* 2/4 */
  .col-lg-3 { width: 75%; } /* 3/4 */
  .col-lg-4 { width: 100%; } /* 4/4 */
  .col-lg-1::after { content: 'col: 1/4' }
  .col-lg-2::after { content: 'col: 2/4' }
  .col-lg-3::after { content: 'col: 3/4' }
  .col-lg-4::after { content: 'col: 4/4' }
}

" resizable="true" style="height: 800px;">

<header id="content" class="row">
  <h2 class="col-lg-4 col-md-4">
    Web Page Development
  </h2>
</header>
<main id="content" class="row">
  <nav class="col-lg-1 col-md-2">
    <ul>
      <li>About the Subject</li>
      <li>Schedule</li>
      <li>Lectures</li>
      <li>Exercises</li>
      <li>Project</li>
    </ul>
  </nav>
  <article class="col-lg-3 col-md-2">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </article>
</main>

</pre>

<span class="note">💡 Test different example widths</span>

=--

<!-- .slide: class="editor" -->

# Příklad

<div data-iframe="assets/examples/responsive/floats6.html"></div>

<div class="note"><a href="assets/examples/responsive/floats6.html">source</a></div>

---

# Summary

- a way to create a Grid system when Flexbox and Grid were not available

<br>

- ***disadvantages***:
  - need to set `overflow` and `clear` properties
  - column height may not fill the row height
  - floating elements are generally better suited for text wrapping, not layout creation
  - gaps between columns must be handled using `padding`

<br>

- Solution: ***Flexbox***
