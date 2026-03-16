# Positioning

  - Manual specification of the object's position on the page
  - Relative
    - Moving the object relatively to its normal position
  - Absolute
    - Placing an object to a particular place independently on the remaining text
  - The `position` property
    - `position: static` \-- normal position (normal flow)
    - `position: relative` \-- relative positioning
    - `position: absolute` \-- absolute positioning
    - `position: fixed` \-- fixed positioning
    - `position: sticky` \-- sticky positioning
  - Affects both the **element iself** and its **child elements**!

---

# Relative positioning

  - The position relative to normal placement
    - `position: relative`
  - The block remains in normal flow; it's just moved
  - The distance from the top left corner
    - `top: length` \- moving down
    - `left: length` \- moving right
  - The distance from the bottom right corner:
    - `bottom: length` \- moving up
    - `right: length` \- moving left
  - May be combined
  - Negative value - reverse direction

---

# Relative positioning - example

<pre class="code-render" default-style="
.word { font-weight: bold; }
" resizable="true">
This is <span class="word">bold</span> text.
</pre>

```html
<style>
    .word {
        font-weight: bold;
    }
</style>
...
This is <span class="word">bold</span> text.
```

=--

# Relative positioning - example

<pre class="code-render" default-style="
.word {
    font-weight: bold;
    position: relative;
    top: 0.5em;
    left: 20px;
}
" resizable="true">
This is <span class="word">bold</span> text.
</pre>

```html
<style>
    .word {
        font-weight: bold;
        position: relative;
        top: 0.5em;
        left: 20px;
    }
</style>
...
This is <span class="word">bold</span> text.
```

---

# Absolute positioning

  - `position: absolute`
  - The object is **removed** from the normal flow
    - Doesn't influence the text in the original position
  - It is placed to a particular poisition on the page
    - It can overlap the content being already on that place
    - It might be necessary to „make space"
  - The distance from the top left corner of the **containing block**
    - `top: length`
    - `left: length`
  - The distance from the bottom left corner
    - `bottom: length`
    - `right: length`

=--

# Absolute positioning - example

<pre class="code-render" default-style="
.word {
    font-weight: bold;
    position: absolute;
    bottom: 0em;
    left: 20px;
}
" resizable="true">
This is <span class="word">bold</span> text.
</pre>

```html
<style>
    .word {
        font-weight: bold;
        position: absolute;
        bottom: 0em;
        left: 20px;
    }
</style>
...
This is <span class="word">bold</span> text.
```

---

# Containing Block

  - Initial containing block is the _Viewport_
  - Elements with position `relative` or `static`
    - The nearest ancestor block is the containing block
  - Elements with position `absolute`
    - The nearest ancestor block with position `relative`, `absolute` or `fixed` is the containing block
  - Elements with position `fixed`
    - Viewport is always the containing block

---

# Coordinate System

  - Normally, the coordinate system is formed by the **Viewport**
  - Elements that have `position: absolute`, `relative` or `fixed`, create a **local coordinate system** for absolute positioning
    - Nested object with `position: absolute` are positioned from within the parent

=--

# Coordinate System (II)

  - Child blocks are positioned within **Viewport** (parent is `static`):

<div class="render-example">

<div style="background: #eef; border: 2px solid #aaf; height: 130px;">
    Parent (position: static)
    <div style="position: absolute; top: 0; right: 0px; background: #fbb; border: 1px solid red; padding: 4px;">child1 (absolute)</div>
    <div style="position: absolute; bottom: 0; left: 0px; background: #bfb; border: 1px solid green; padding: 4px; z-index: 1000">child2 (absolute)</div>
</div>

</div>

```html
<div id="parent">
    Parent (position: static)
    <div id="child1" style="position: absolute">...</div>
    <div id="child2" style="position: absolute">...</div>
</div>
```

=--

# Coordinate System (III)

  - Child blocks are positioned within **parent block** (parent is `relative`):

<div class="render-example">

<div style="background: #eef; border: 2px solid #aaf; height: 130px; position: relative;">
    Parent (position: relative)
    <div style="position: absolute; top: 0; right: 0px; background: #fbb; border: 1px solid red; padding: 4px;">child1 (absolute)</div>
    <div style="position: absolute; bottom: 0; left: 0px; background: #bfb; border: 1px solid green; padding: 4px; z-index: 1000">child2 (absolute)</div>
</div>

</div>

```html
<div id="parent" style="position: relative">
    Parent (position: relative)
    <div id="child1" style="position: absolute">...</div>
    <div id="child2" style="position: absolute">...</div>
</div>
```

---

<!-- .slide: class="editor" -->

# Absolute positioning -- containing blocks

<div data-iframe="assets/examples/absolute.html"></div>

---

<!-- .slide: class="editor" -->

# Fixed positioning

<div data-iframe="assets/examples/fixed.html"></div>

---

<!-- .slide: class="editor" -->

# Sticky positioning

<div data-iframe="assets/examples/sticky.html"></div>

---

# Positioned Element Width and Height

  - The equation for width:


<div class="textbox">

**left** + margin-left + border-left-width + padding-left \
\+ width \
\+ padding-right + border-right-width + margin-right + **right** \
\= _containing_block_width_

</div>

  - The `auto` values for `left` and `top` are derived from _static position_
  - Computation of multiple `auto` values is defined in the [specification](http://www.w3.org/TR/CSS21/visudet.html#abs-non-replaced-width)
  - The **height** is computed **analogously**

---

# Element overlaping

  - Two elements may overlap (relative or absolute positioning)
  - Normally, the later specified object overlaps the earlier object
  - This can be changed using the `z-index` property
    - `z-index: 10`
    - The number gives the Z coordinate of the object (the higher number the „higher" placed is the object)
    - If not specified, **0** is used

---

# Overlaping: example

<pre class="code-render" default-style="
.box { padding: 1em; border: 2px solid; }
" resizable="false" style="height: 10em">
<div style="height: 120px; position: relative; background: #f5f5f5;">
    <div class="box" style="position: absolute; top: 15px; left: 20px; background: #bbf; border-color: blue;">First box</div>
    <div class="box" style="position: absolute; top: 50px; left: 60px; background: #fbb; border-color: red;">Second box</div>
</div>
</pre>

```html
<div style="height: 4em; position: relative">
    <div class="box" style="position: absolute;
         top: 30px; left: 180px">
         First box</div>
    <div class="box" style="position: absolute;
         top: 60px; left: 200px">
         Second box</div>
</div>
```

=--

# Overlaping: example

<pre class="code-render" default-style="
.box { padding: 1em; border: 2px solid; }
" resizable="false" style="height: 10em">
<div style="height: 120px; position: relative; background: #f5f5f5;">
    <div class="box" style="position: absolute; top: 15px; left: 20px; background: #bbf; border-color: blue; z-index: 1;">First box</div>
    <div class="box" style="position: absolute; top: 50px; left: 60px; background: #fbb; border-color: red;">Second box</div>
</div>
</pre>

```html
<div style="height: 4em; position: relative">
    <div class="box" style="position: absolute;
         top: 30px; left: 180px; z-index: 1">
         First box</div>
    <div class="box" style="position: absolute;
         top: 60px; left: 200px">
         Second box</div>
</div>
```

---

# Content hiding

```html
This is <span style="...">invisible</span> text.
```

  1. `display: none` -- the element is totally ignored during layout and rendering

<div class="textbox">
This is <span style="display: none">invisible</span> text.
</div>

  2. `visibility: hidden` -- the element is considered during layout but not displayed

<div class="textbox">
This is <span style="visibility: hidden">invisible</span> text.
</div>

---

# Why to hide the text

  1. `display: none`
     - The elements displayed in browsers with no CSS support (alternative navigation, auxiliary labels, ...)
     - Element intended for other media types (e.g. for printing)
  2. `visibility: hidden`
     - The elements that may be displayed later (scripting)
