# 🎨 CSS - Medium Questions From Notes

> **Topics from Notes Covered:** Flexbox, CSS Grid, Horizontal Scrolling Implementation.

---

### Q1: Flexbox vs CSS Grid
**Question (From Notes):** When should you use Flexbox vs Grid?

**Answer:**
- **Flexbox (1-Dimensional)**: Designed for laying items out along a **single axis** (either a row OR a column).
  - *Best For*: Navigation bars, aligning items, distributing space in a toolbar, centering components.
- **CSS Grid (2-Dimensional)**: Designed for laying items out across **both rows and columns simultaneously**.
  - *Best For*: Entire page layout systems, photo galleries, dashboards, multi-column card grids.

```css
/* Flexbox 1D Example */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/* CSS Grid 2D Example */
.dashboard {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}
```

---

### Q2: Horizontal Scrolling Implementation in CSS
**Question (From Notes):** How do you implement horizontal scrolling in CSS?

**Answer:**
Using `display: flex`, `overflow-x: auto`, and `scroll-snap-type`:

```css
.horizontal-scroll-wrapper {
  display: flex;
  gap: 16px;
  overflow-x: auto;
  overflow-y: hidden;
  white-space: nowrap;
  scroll-snap-type: x mandatory;
  -webkit-overflow-scrolling: touch; /* Momentum scroll on iOS */
  padding: 16px;
}

.scroll-card {
  flex: 0 0 260px; /* Don't grow, don't shrink, fixed width */
  scroll-snap-align: start;
  height: 160px;
  background: #3b82f6;
  border-radius: 12px;
}

/* Hide scrollbar cleanly */
.horizontal-scroll-wrapper::-webkit-scrollbar {
  display: none;
}
.horizontal-scroll-wrapper {
  -ms-overflow-style: none;
  scrollbar-width: none;
}
```
