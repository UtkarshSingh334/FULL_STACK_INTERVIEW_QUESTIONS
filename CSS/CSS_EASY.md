# 🎨 CSS - Easy Questions

> **Topics Covered:** What is CSS, Types of CSS (Inline, Internal, External), CSS Box Model, Margin vs Padding, CSS Selectors & Specificity, Text & Font Styling, Colors & Units (`px`, `rem`, `em`, `%`, `vh`, `vw`), Display Property (`block`, `inline`, `inline-block`, `none`).

---

### Q1: What is CSS and What are the 3 Ways to Apply It?
**Question:** What is CSS? Explain the 3 methods to include CSS in an HTML document.

**Answer:**
- **CSS (Cascading Style Sheets)** is used to style and lay out HTML documents (colors, layouts, fonts, animations).
- **Three Ways to Apply CSS:**
  1. **Inline CSS**: Applied directly to the HTML element using the `style` attribute.
     ```html
     <h1 style="color: blue; font-size: 24px;">Hello</h1>
     ```
  2. **Internal (Embedded) CSS**: Defined inside `<style>` tags within the `<head>` section.
     ```html
     <style>
       h1 { color: blue; }
     </style>
     ```
  3. **External CSS**: Linked via external `.css` file (Recommended for separation of concerns and caching).
     ```html
     <link rel="stylesheet" href="styles.css">
     ```

---

### Q2: The CSS Box Model ⭐
**Question:** Explain the CSS Box Model with all its components. What is `box-sizing: border-box`?

**Answer:**
Every HTML element is rendered as a rectangular box consisting of 4 concentric layers:
1. **Content**: The actual text, image, or child elements.
2. **Padding**: Transparent space between the content and the border.
3. **Border**: The outline surrounding the padding.
4. **Margin**: Transparent space outside the border separating the element from neighbors.

```
+-----------------------------------+
|              MARGIN               |
|   +---------------------------+   |
|   |          BORDER           |   |
|   |   +-------------------+   |   |
|   |   |      PADDING      |   |   |
|   |   |   +-----------+   |   |   |
|   |   |   |  CONTENT  |   |   |   |
|   |   |   +-----------+   |   |   |
|   |   +-------------------+   |   |
|   +---------------------------+   |
+-----------------------------------+
```

**`content-box` vs `border-box`:**
- `content-box` (Default): Total Width = `width + padding-left + padding-right + border-left + border-right`.
- `border-box` (Recommended): Total Width = `width` (Padding and border are absorbed inside the defined width).

```css
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
```

---

### Q3: Margin vs Padding
**Question:** What is the difference between Margin and Padding?

**Answer:**
| Criteria | Margin | Padding |
| :--- | :--- | :--- |
| **Location** | Outside the element's border | Inside the element's border |
| **Background Color**| Transparent (shows parent element background) | Inherits the element's own background color |
| **Clickable Area** | Not part of element's click target | Part of element's active clickable hitbox |
| **Collapsing** | Vertical margins between sibling blocks can collapse | Never collapses |

---

### Q4: CSS Units: `px` vs `rem` vs `em` vs `%` vs `vh` / `vw`
**Question:** Compare relative and absolute CSS units. When should you use `rem` over `em`?

**Answer:**
- **`px` (Pixels)**: Fixed, absolute unit. Does not adapt to user browser font-size preferences.
- **`rem` (Root EM)**: Relative to the root `<html>` element's `font-size` (default `16px`). `1.5rem = 24px`. Ideal for responsive typography and spacing.
- **`em`**: Relative to the `font-size` of its **immediate parent element** (can compound unintentionally in nested elements).
- **`%`**: Relative to the parent element's dimensions.
- **`vw` / `vh`**: Viewport Width / Viewport Height ($1vw = 1\%$ of viewport width).

---

### Q5: CSS Selector Specificity Hierarchy
**Question:** How does CSS determine which rule takes precedence when multiple selectors target the same element?

**Answer:**
Specificity is calculated as a 4-part score: `(Inline, IDs, Classes/Attributes/Pseudo-classes, Elements/Pseudo-elements)`:
1. `!important`: Overrides all normal specificity rules.
2. **Inline styles** (`style="..."`): `(1, 0, 0, 0)`
3. **IDs** (`#header`): `(0, 1, 0, 0)`
4. **Classes, Attributes, Pseudo-classes** (`.btn`, `[type="text"]`, `:hover`): `(0, 0, 1, 0)`
5. **Element & Pseudo-elements** (`div`, `p`, `::before`): `(0, 0, 0, 1)`
6. **Universal Selector (`*`)**: `(0, 0, 0, 0)`
