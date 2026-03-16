<!-- .slide: class="section" -->

<header>
  <h1>CSS Language</h1>
  <p>Introduction, Principles</p>
</header>

---

# CSS

- CSS = <i>Cascading Style Sheet</i>
- *Standard* language for creating style sheets
  - **[Specification](https://www.w3.org/Style/CSS/)** maintained by W3C (World Wide Web Consortium), more readable version: **[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS)**

<br>

- **Origins (1994 - 1996)** -- birth of CSS, first specification (*CSS1*), basic styles for text and colors
- **Development (1998 - 2000)** -- *CSS2* introduces positioning, layers, media types
  - ⚠️ inconsistent browser support
- **Modularization and CSS3 (2001 - 2010)** -- development split into ***modules*** (*CSS 3*)
  - flexbox, animations, advanced selectors, responsive media queries
- **Modern Layouts (2011 - 2020)** -- greater focus on responsive design and mobile web
  - 2011 -- [CSS 2.1 W3C Recommendation](https://www.w3.org/TR/2011/REC-CSS2-20110607/) -- ✅ stable, supported by browsers
  - CSS Grid, custom properties (variables)
- **Present (2021 - today)** -- container queries, subgrid, :has() selector, native nesting, Houdini API
  - *CSS 3+* modules

---

# Style Sheet

- ***sequence of rules*** concerning various *elements* that determine their ***properties***
  - e.g. color and font weight of `<p>` elements
  - typically multiple rules for each element

<br>

- sources of style sheets:
   1. *author style* (prepared by the page creator)
   2. user style (<i>user stylesheets</i>) - user's own definitions
   3. browser style (<i>user agent styles</i>)

<br>

- relevant rules are arranged into a ***cascade***
  - fully define the final appearance (properties) of each element

---

# Linking to an HTML Document

- ***external***, ***internal***, and ***inline*** style sheets

```html
<head>
  <!-- external style sheet -->
  <link rel="stylesheet" type="text/css" href="style.css"> 
  
  <!-- internal style sheet -->
  <style>
    /* CSS language inside HTML document */
    p {
      color: gray;
    }
  </style>
</head>

<body>
  <!-- inline style sheet -->	
  <p style="font-weight: bold; font-style: italic;"></p>
</body>
```

- ***beware of priorities!*** -- more on this later...

---

# CSS Syntax

```css
/* rule */
selector { 
  property: value;
  property: value;
  ...
}

/* another rule */
selector {
  property: value;
  property: value;
  ...
}

... 
```

- ***selector*** -- specifies which elements the rule applies to
- ***property*** -- defines visual (or other) characteristics of the selected elements