# Floating blocks

  - Object that are flowed by the surrounding text
  - Creating a floating object:
    - `float: left` or
    - `float: right`
  - Floating elements become automaticaly **block** elements
  - The floating object is
    - Removed from the normal text flow (doesn't influence the text on the original place)
    - Shifted to the border of the parent element
  - Different way of width computation
    - It is better to set an explicit width
    - If not set, it is automaticaly computed (shring-to-fit algorithm)

---

<!-- .slide: class="editor" -->

# Creating a Floating Object

<div data-iframe="assets/examples/float0.html"></div>

=--

<!-- .slide: class="editor" -->

# Creating a Floating Object -- Width

<div data-iframe="assets/examples/float1.html"></div>

=--

<!-- .slide: class="editor" -->

# Creating a Floating Object -- Width

<div data-iframe="assets/examples/float2.html"></div>

---

<!-- .slide: class="editor" -->

# Float and In-Flow Block Size

<div data-iframe="assets/examples/float3.html"></div>

---

# Clear

  - The floating objects are placed by the browser
    - Side by side to the appropriate margin
    - When there is no space then below each other
    - => The floating object can horizontally overflow the flowing text
  - When some text shouldn't flow along the floating objects:
    - `clear: left | right | both`
  - First, previous floating object are placed, then the text is placed below

<pre class="code-render" default-style="
* {
  font-family: sans-serif;
}
.box {
    float: left;
    width: 8em;
    background: #ddf;
    border: 1px solid #aaf;
    margin-right: 1em;
    padding: 0.5em;
}
.cleared { clear: both; border-top: 2px solid red; padding-top: 0.3em; }
" resizable="true" style="height: 8em; width: 90%; margin: auto">
<div class="box">Float 1</div>
<div class="box">Float 2</div>
<p>This paragraph has no clear — wraps around the floats.</p>
<p class="cleared">This paragraph has <code>clear: both</code> — starts below both floats.</p>
</pre>

=--

<!-- .slide: class="editor" -->

# Clear property

<div data-iframe="assets/examples/clear1.html"></div>

=--

<!-- .slide: class="editor" -->

# Clear property

<div data-iframe="assets/examples/clear2.html"></div>

---

# Containing Block Height

  - When a block has `height:auto`, its height depends on its contents
  - For `overflow: visible`
    - Only in-flow content is considered
    - If the block contains floating blocks only, it has **zero height** in the result
  - Otherwise (e.g. `overflow: hidden`)
    - Floating content is considered too

<pre class="code-render" style="height: 12em" default-style="
* {
  font-family: sans-serif;
}
.contents {
    border: 5px solid blue;
    margin-bottom: 1em;
}
.col {
    float: left;
    background: gray;
    color: white;
    padding: 0.5em;
    margin-right: 0.3em;
}
.visible { overflow: visible; }
.hidden { overflow: hidden; }
" resizable="true" style="height: 270px; width: 90%; margin: auto">
<p><strong>overflow: visible</strong> — blue border collapses to zero height:</p>
<div class="contents visible">
    <div class="col">Column 1</div>
    <div class="col">Column 2</div>
</div>
<p style="clear:both"><strong>overflow: hidden</strong> — blue border wraps the floats:</p>
<div class="contents hidden">
    <div class="col">Column 1</div>
    <div class="col">Column 2</div>
</div>
<p style="clear:both">Next contents</p>
</pre>
