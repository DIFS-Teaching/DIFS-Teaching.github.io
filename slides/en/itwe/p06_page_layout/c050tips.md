<!-- .slide: class="section" -->

# CSS Usage Tips

---

# External Style Definitions

  - Use external style definitions 
    - Shared style sheets for a set of documents
  - Multiple style sheets may be used
  
```html
<link ="" rel="stylesheet" src="common.css" type="text/css"/>
<link ="" rel="stylesheet" src="section.css" type="text/css"/>
```

---

# Distinguish between `id` and `class`

  - `id` attribute 
    - For unique elements
    - Easier to use (more specific selector)
    - Clearer style sheet
  - `class` attribute 
    - For repeating elements

---

# Class and id names

  - Use descriptive class and id names 
    - Should describe the **meaning** , not the appearance
    - Bad: `rightcolumn`, `redtext`
    - Correct: `menu`, `important`
  - Use a small set of class names 
    - Many names are hard to remember
    - Use context selectors

```css
p span.first {...} /* first letter of the paragraph */ 
p.first {...} /* first paragraph in the article */ 
li.first {...} /* first list item */ 
```

---

# Context Selectors

  - Don't create useless classes, use context selectors
  - Wrong:

```html
<h2 class="articleheading">Heading</h2>
<p class="articlepar">...</p>
 ...
<p class="articlepar">...</p>
``` 
```css
.articleheading { ... }
.articlepar { ... }
```

---

# Context Selectors

  - Right:

```html
<div class="article">
   <h2>Title</h2>
   <p>...</p>
   ...
   <p>...</p>
</div>
``` 
```css
.article h2 { ... }
.article p { ... }
```

---

# Context Selectors

  - Wrong:

```html
<ul>
<li class="menu">...</li>
<li class="menu">...</li>
 ...
<li class="menu">...</li>
</ul>
```

```html
.menu { ... }
```

---

# Context Selectors

  - Right:

```html
<ul class="menu">
<li>...</li>
<li>...</li>
 ...
<li>...</li>
</ul>
```

```css
ul.menu li { ... }
```

---

# Combine Classes

  - Use more classes for one element
    - `class="importantmessage"` vs. `class="message important"`
  - Cascade the rules
  
```html
h1, h2 {
   font-family: "Arial CE", Arial, sans-serif;
   font-weight: bold;
}
h1 {
   font-size: 200%
}
h2 {
   font-size: 160%
}
```

---

# Writing the Style Sheet

  - Write with a clear style
  - Choose some selector order 
    - Elements, id, classes, ...
    - Or according to the page organization
  - Choose some property specification order 
    - E.g. sizes, margins, position, colors and borders
  - Write rules to separate lines 
    - Easy to copy
  - Use comments `/* comment */`
