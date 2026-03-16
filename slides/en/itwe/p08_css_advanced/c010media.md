<!-- .slide: class="section" -->
 
<header>
  <h1>Media Queries</h1>
  <p>Media Type, Media Features, Printed Media</p>
</header>

---

# Media Queries

- allows styles to apply only under certain conditions
- use the ***@media*** rule for conditional style definitions
- [Media Queries Level 3](https://www.w3.org/TR/mediaqueries-3/) (W3C Recommendation)
  - [Media Queries Level 4](https://www.w3.org/TR/mediaqueries-4/) (W3C Candidate Recommendation Draft)

```css
@media not|only mediatype and (expressions) {
  /* CSS rules */
}
```

- ***not***: negates the entire rule
- ***only***: older browsers will ignore the construction
- ***mediatype***: type of media/device
  - screen, print, speech, all, …
- ***expressions***: conditions for the rule (screen size, …) -- ***media features***

---

# Media Types (historical)

- **defined in [CSS Level 2](https://www.w3.org/TR/CSS2/media.html#q7.0)**
  - *tty* -- for teletype terminals, character-based displays
  - *tv* -- for television devices, low-resolution screens
  - *projection* -- for projectors / presentations
  - *handheld* -- for early mobile devices / PDAs
  - *braille* -- for refreshable braille displays
  - *embossed* -- for braille printers
  - *aural* -- for speech synthesizers / screen readers
  - *speech* -- modern replacement for aural, largely unsupported

- **obsolete HW** -- devices like teletype, braille embossers, or PDAs are largely gone. 
- **device convergence** -- modern devices combine features of old categories
- **limited browser support** -- legacy types were rarely or never fully supported
- **better alternatives available** -- media features (width, pointer, hover, prefers-*)

---

# Media Types (current)

- **[Media Queries Level 4](https://drafts.csswg.org/mediaqueries-4/#media-type) uses the following types:** 
  - *all* -- applies to all devices and media (default)
  - *screen* -- for computer screens, tablets, smartphones, etc.
  - *print* -- for printed documents and print preview

```css
/* import CSS file based on media type at the beginning of another CSS file */
@import "screen.css" screen;
@import "print.css" print;
@import "common.css" all;
```

```html
<!-- link CSS file based on media type -->
<link rel="stylesheet" type="text/css" media="print">
```

<br>

- they use ***media features*** for responsiveness

---

# Media Features: Dimension

- *width* -- viewport width
- *height* -- viewport height
- *min-width* / *max-width* -- min/max viewport width (most common for breakpoints)
- *min-height* / *max-height* -- min/max viewport height

<br>

- *device-width* / *device-height*-- dimensions of the entire device screen (less commonly used)

<br>

- the modern solution that makes using device-width unnecessary in most cases:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

<span class="note"><a href="https://www.w3schools.com/css/css_rwd_viewport.asp">W3Schools example</a><span>

---

# Media Features: Other

  - *orientation* -- `portrait` or `landscape`
  - *resolution* -- pixel density (dpi or dppx)
  - *aspect-ratio* -- width-to-height ratio of the viewport
  - *pointer* -- type of pointing device (`none`, `coarse` -- touchscreen, `fine` -- mouse. stylus )
  - *hover* -- whether the primary input can hover (`none` / `hover`)
  - *prefers-color-scheme* -- `light` or `dark` mode
  - *prefers-reduced-motion* -- prefers less animation
  - *prefers-contrast* -- high / low contrast

---

# Printed Media

- targets printed documents and print preview in browsers.
- CSS rules are wrapped inside a media query to style content specifically for printing

```css
@media screen {
    body {
        font-family: sans-serif;
        font-size: 12pt;
    }
}

@media print {
    body {
        font-family: serif;
        font-size: 10pt;
        color: black;
        background: white;
    }
    nav, .sidebar, .ads {
      display: none; /* hide unnecessary elements in print */
    }
}
```

---

# Printed Media: Pagination

- **older CSS2 properties:**
  - *page-break-before*: `auto` | `always` | `avoid` | `left` | `right`
  - *page-break-after*: `auto` | `always` | `avoid` | `left` | `right`
  - *page-break-inside*: `auto` | `avoid`

```html
...
<div class="slide">
    Slide content
</div>
...
```

```css
div.slide {
    page-break-after: always; /* break after */
    page-break-inside: avoid; /* avoid breaking inside */
}
```

---

# Printed Media: Pagination

- **[CSS Fragmentation Module Level 3](https://www.w3.org/TR/css-break-3/) (W3C Candidate Recommendation)**
  - *break-before*: `auto` | `page` | `column` | `avoid` | `left` | `right`;
  - *break-after*: `auto` | `page` | `column` | `avoid` | `left` | `right`;
  - *break-inside*: `auto` | `avoid` | `avoid-page` | `avoid-column`;

- **values:**
  - *auto* -- uses default behavior (breaking rules according to context)
  - *page* -- inserts a page break
  - *column* -- inserts a column break (in multi-column layout)
  - *avoid* -- prevents element splitting if possible
  - *left* / *right* -- for printing: inserts a page that will start on the left/right

<br>

- adds support for multi-column layouts (*`column-count: 3;`*)

=--

# Support for Muluti-column Layouts

- additionally, it supports multi-column layouts (*`column-count: 3;`*)

```css
.container {
  column-count: 3;
  column-gap: 20px;
}

h2 {
  break-before: column;  /* every heading starts new column */
}

section {
  break-inside: avoid;   /* section will not be splitted into columns */
}
```

---

# @page Rule

- rule which ses properties of printed pages
- **[CSS Paged Media Module Level 3](https://www.w3.org/TR/css-page-3/) (W3C Working Draft)**

```css
@media print {
  @page {
    size: A4 landscape;  /* A4 page, landscape orientation */
    margin: 2cm;         /* page margins */
  }

  @page :first {
    margin-top: 4cm;     /* extra space for title page */
  }

  @page :left {
    margin-left: 3cm;    /* wider left margin */
  }

  @page :right {
    margin-right: 3cm;   /* wider right margin */
  }
}
```

---

# Printed Media: Recommendation

- **Hide non-essential elements:** display: none for navigation, ads, and sidebars.
- **Control page breaks:** use break-before, break-after, or break-inside: avoid for sections.
- **Optimize typography:** adjust font-size, line-height, and font-family for readability.
- **Simplify colors:** set color: black and background: white for legibility and ink saving.
- **Manage images:** scale or hide large images to fit pages neatly.
- **Set page size and margins:** use @page rule (size, margin) for consistent layout.
- **Avoid complex layouts:** remove floats, columns, or interactive elements that do not print well.
- **Test print preview:** always check how content breaks across pages and adjust accordingly.

