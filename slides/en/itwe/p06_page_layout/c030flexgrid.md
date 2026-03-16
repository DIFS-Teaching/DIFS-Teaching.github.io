# Flexbox

- Mostly for local layouts 
  - Forms, list items, ...
- Parent element is used as a **flex container**
  - By setting `display: flex`
  - We define the `main axis` and the `cross axis`
- The child elements become the **flex items**

---

# Flex Container Properties

- [flex-direction](assets/examples/flex1.html) \-- main axis direction
- [flex-wrap](assets/examples/flex2.html) \-- content wrapping to more rows/columns
- [justify-content](assets/examples/flex3.html) \-- content justification in the row/column
- [align-items](assets/examples/flex4.html) \-- item alignment

---

# Item Properties

- [flex:](assets/examples/flex5.html) `<flex-grow>` `<flex-shrink>` `<flex-basis>`
- `flex-grow` \-- how the item grows when there is more space available 
  - `flex-grow: 0` \-- does not grow at all
  - `flex-grow: 2` \-- weight 2, relative to the remaining weights
- `flex-shrink` \-- how the item shrinks when there is not enough space 
  - `flex-shrink: 1`
- `flex-basis` \-- initial main size 
  - `flex-basis: auto`
  - `flex-basis: content`
  - `flex-basis: 10em`
  - `flex-basis: 40%`

---

# Grid layout

- Parent element is the **grid container**
  - By setting `display: grid`
  - We set the number of grid rows and columns 
    - Explicit (template) nebo implicit (auto)
    - The `fr` (fraction) length unit
  - Named areas may be created (multiple grid cells)
- Grid position is set for child elements 
  - `grid-row-start`, `grid-row-end` (`grid-row`)
  - `grid-column-start`, `grid-column-end` (`grid-column`)
  - or `grid-area` ([demo](assets/examples/grid.html))
- [Description and demo on MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout)
- [Detailed description](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Basic_Concepts_of_Grid_Layout)
