# 🎨 CSS - Medium Questions

> **Topics Covered:** Flexbox (axes, centering, properties), CSS Grid (template columns, auto-fill/auto-fit, gap), Flexbox vs Grid, CSS Positioning (`static`, `relative`, `absolute`, `fixed`, `sticky`), `z-index` & Stacking Context, Media Queries & Mobile-First Design, Pseudo-classes (`:hover`, `:focus`, `:nth-child`) vs Pseudo-elements (`::before`, `::after`), Visibility (`display: none` vs `visibility: hidden` vs `opacity: 0`).

---

### Q1: Flexbox Deep Dive ⭐
**Question:** What is CSS Flexbox? Explain its main axes and how to center an element horizontally and vertically.

**Answer:**
Flexbox is a 1-dimensional layout model designed to distribute space along either a row (horizontal) or a column (vertical).

- **Main Axis**: Defined by `flex-direction` (`row` [default], `column`, `row-reverse`, `column-reverse`).
- **Cross Axis**: Perpendicular to the main axis.
- **Parent (Container) Properties:** `display: flex`, `flex-direction`, `justify-content` (main axis), `align-items` (cross axis), `flex-wrap`, `gap`.
- **Child (Item) Properties:** `flex-grow`, `flex-shrink`, `flex-basis` (shorthand `flex: 1 1 auto`), `align-self`, `order`.

**Perfect Center in Flexbox:**
```css
.center-container {
  display: flex;
  justify-content: center; /* Main axis center */
  align-items: center;     /* Cross axis center */
  height: 100vh;
}
```

---

### Q2: CSS Grid Deep Dive ⭐
**Question:** What is CSS Grid? How does it differ from Flexbox? Create a responsive 3-column layout.

**Answer:**
- **CSS Grid** is a **2-dimensional** layout system (handles both rows and columns simultaneously).
- **Flexbox vs Grid:**
  - *Flexbox*: 1D (content-first, ideal for navigation bars, item lists, linear button groups).
  - *Grid*: 2D (layout-first, ideal for whole page structures, photo galleries, dashboards).

**Responsive Auto-Fitting Grid without Media Queries:**
```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 20px;
}
```

---

### Q3: CSS Positioning: `static` vs `relative` vs `absolute` vs `fixed` vs `sticky`
**Question:** Explain all CSS position values with their coordinate anchors.

**Answer:**
1. **`static`** (Default): Follows normal document flow. `top`, `bottom`, `left`, `right`, `z-index` have no effect.
2. **`relative`**: Positioned relative to its normal position in document flow without altering space occupied. Serves as anchor for `absolute` children.
3. **`absolute`**: Removed from normal document flow. Positioned relative to the **nearest ancestor with position other than `static`** (or `<html>`).
4. **`fixed`**: Removed from document flow. Anchored relative to the **browser viewport**. Remains stationary during scrolling (e.g., sticky headers, modals).
5. **`sticky`**: Hybrid. Acts as `relative` until a specified scroll threshold is reached, then sticks like `fixed` within its parent container.

```css
/* Sticky Table Header */
th {
  position: sticky;
  top: 0;
  background: #ffffff;
  z-index: 10;
}
```

---

### Q4: `z-index` and Stacking Context
**Question:** How does `z-index` work? Why does `z-index: 9999` sometimes fail to bring an element to the front?

**Answer:**
- `z-index` controls the 3D stacking order along the Z-axis for elements that have an explicit `position` (`relative`, `absolute`, `fixed`, or `sticky`) or are flex/grid items.
- **Why it fails (Stacking Context):**
  A child element's `z-index` is evaluated **only within its parent's stacking context**. If Parent A has `z-index: 1` and Parent B has `z-index: 2`, no child inside Parent A (even with `z-index: 99999`) can ever appear on top of Parent B.
- **What triggers a new Stacking Context:**
  - `position: relative/absolute` with `z-index` other than `auto`.
  - `position: fixed` or `sticky`.
  - `opacity` less than `1`.
  - `transform`, `filter`, `perspective`, `clip-path` properties.

---

### Q5: `display: none` vs `visibility: hidden` vs `opacity: 0`
**Question:** Compare `display: none`, `visibility: hidden`, and `opacity: 0`.

**Answer:**
| Property | Occupies Space in DOM Layout | Triggers Reflow / Repaint | Accessible to Screen Readers | Clickable / Interactive | CSS Transitions |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`display: none`** | ❌ Removed from layout flow | Reflow + Repaint | ❌ No | ❌ No | ❌ No |
| **`visibility: hidden`** | ✅ Retains space | Repaint only | ❌ No (usually ignored) | ❌ No | ❌ No (instant flip) |
| **`opacity: 0`** | ✅ Retains space | Repaint / Composite | ✅ Yes | ✅ Yes (unless `pointer-events: none`) | ✅ Smooth transition |

---

### Q6: Pseudo-Classes vs Pseudo-Elements
**Question:** What is the difference between pseudo-classes (`:`) and pseudo-elements (`::`)?

**Answer:**
- **Pseudo-Class (`:`)**: Selects an element based on its **state or structural position** (e.g., `:hover`, `:focus`, `:active`, `:disabled`, `:nth-child(2n)`, `:not(.active)`).
- **Pseudo-Element (`::`)**: Creates an **abstract sub-element** of the selector to style specific parts (e.g., `::before`, `::after`, `::placeholder`, `::first-letter`, `::selection`).

```css
/* Tooltip using ::after */
.tooltip {
  position: relative;
}
.tooltip::after {
  content: attr(data-tip);
  position: absolute;
  bottom: 100%;
  left: 50%;
  transform: translateX(-50%);
  background: #333;
  color: #fff;
  padding: 4px 8px;
  border-radius: 4px;
  opacity: 0;
  transition: opacity 0.2s;
}
.tooltip:hover::after {
  opacity: 1;
}
```

---

### Q7: Media Queries & Mobile-First Responsive Design
**Question:** What is mobile-first design and how do you implement it with media queries?

**Answer:**
- **Mobile-First Design**: Writing base styles for mobile devices first using `min-width` queries to progressively enhance layouts for larger screens.

```css
/* Base styles (Mobile default: 1 column) */
.container {
  width: 100%;
  padding: 16px;
}

/* Tablet (min-width: 768px) */
@media (min-width: 768px) {
  .container {
    max-width: 720px;
    margin: 0 auto;
  }
}

/* Desktop (min-width: 1024px) */
@media (min-width: 1024px) {
  .container {
    max-width: 960px;
  }
}
```
