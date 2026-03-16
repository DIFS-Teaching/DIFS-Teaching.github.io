
# Property inheritance

  * Some property values are inherited by the child elements
    - *When not explicitly specified*

```html
<p class="intro concl">Following text is
    <span class="imp">important</span></p>
```

```css
p { color: red; border: 1px solid blue; }
``` 

  * The text color applies to the child element too
  * Only the parent element `<p>` has the border
  * The [CSS specification](https://www.w3.org/TR/CSS22/propidx.html) defines which properties are inherited

---

# Typical Usage of Inheritance

```css
body {
    color: white;
    background-color: black;
}

h1 {
    color: red;
}
``` 

* All the text will be white 
  * All the elements inherit their color from the `body` element
* Only the headings (and their descendant elements) will be red 
  * We define red color for `h1`

---

# The `inherit` value

  * Any property can have a special `inherit` value
  * The property value is then always inherited from the parent element

---
<!-- .slide: class="normal centered fullspace" data-transition="slide-in fade-out" -->

# Example

<pre class="code-render" default-style="" resizable="true" style="height: 400px">
<style>
#menu { border: 3px #057205ff solid; }
</style>
<div id="menu">
	<h1>Menu</h1>
	<p>First paragraph</p>
	<p>Second paragraph</p>
</div>
</pre>


```html
<div id="menu">
	<h1>Menu</h1>
	<p>First paragraph</p>
	<p>Second paragraph</p>
</div>
```
```css
#menu { border: 3px #057205ff solid; }
```

---
<!-- .slide: class="normal centered fullspace" data-transition="fade-in fade-out" -->

# Example (II)

<pre class="code-render" default-style="" resizable="true" style="height: 400px">
<style>
#menu { border: 3px #057205ff solid; }
#menu p { border: inherit; }
</style>
<div id="menu">
	<h1>Menu</h1>
	<p>First paragraph</p>
	<p>Second paragraph</p>
</div>
</pre>

```html
<div id="menu">
	<h1>Menu</h1>
	<p>First paragraph</p>
	<p>Second paragraph</p>
</div>
```
```css
#menu { border: 3px #057205ff solid; }
#menu p { border: inherit; }
```
---
<!-- .slide: class="normal centered fullspace" data-transition="fade-in slide-out" -->

# Example

<pre class="code-render" default-style="" resizable="true" style="height: 400px">
<style>
#menu { border: 3px #057205ff solid; }
#menu p { border-style: dashed; border-color: inherit; }
</style>
<div id="menu">
	<h1>Menu</h1>
	<p>First paragraph</p>
	<p>Second paragraph</p>
</div>
</pre>

```html
<div id="menu">
	<h1>Menu</h1>
	<p>First paragraph</p>
	<p>Second paragraph</p>
</div>
```
```css
#menu { border: 3px #057205ff solid; }
#menu p { border-style: dashed; border-color: inherit; }
```
