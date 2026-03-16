# Visual Style in HTML

- **HTML 4**
  - contained presentational tags (*`<font>`*, *`<center>`*, *`<big>`*, ...)
  - and attributes (*`bgcolor`*, *`align`*, *`border`*, ...)

<br>

- 🔴 ***disadvantages:***
  - cluttered and hard-to-maintain code
  - changing appearance means editing every HTML file → tedious and error-prone
  - document cannot be easily reformatted for other outputs (mobile version, print, readers)
  - poor accessibility → for example, `<b>` does not tell a reader why text is highlighted
  - **dynamically generated content**
    - program must generate both content and appearance
    - changing appearance requires changing the program

=--

<!-- .slide: class="editor" -->

# Visual Style in HTML -- Example

<div data-iframe="assets/examples/html4/html4.html"></div>

<div class="note"><a href="assets/examples/html4/html4.html">source</a></div>

---

# Separation of Appearance from Content

- **HTML 5**
  - describe the ***structure*** and ***meaning*** of content
  - appearance described separately in a ***style sheet*** (*Cascading Style Sheet*)

<br>

- 🟢 <span style="color: green;">**advantages:**</span>
  - **separation of content and presentation** -- HTML handles structure and meaning, CSS handles appearance
  - **easy maintenance** -- changing one CSS class updates appearance across all web pages
  - **reusability** -- the same styles can be applied to different documents
  - **flexibility** -- different styles for different devices (mobile, print, dark mode)
  - **advanced features** -- animations, responsive design, variables, grid/flexbox – HTML alone cannot do this

=--

<!-- .slide: class="editor" -->

# Separation of Appearance from Content -- Example

<div data-iframe="assets/examples/html4/html5.html"></div>

<div class="note"><a href="assets/examples/html4/html5.html">source</a></div>