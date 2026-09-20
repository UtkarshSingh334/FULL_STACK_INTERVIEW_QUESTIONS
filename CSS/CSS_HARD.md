# 🎨 CSS - Hard Questions From Notes

> **Topics from Notes Covered:** Stacking Contexts in Position, Advanced Grid & Flex performance.

---

### Q1: CSS `position: sticky` and Stacking Contexts
**Question (From Notes):** Why does `position: sticky` fail to work sometimes? How does stacking context relate to positioning?

**Answer:**
**Common reasons `position: sticky` fails:**
1. **Ancestor with `overflow: hidden`, `overflow: auto`, or `overflow: scroll`**: Clips the sticky scroll boundary.
2. **Missing top/bottom threshold**: Must declare `top: 0`, `bottom: 0`, etc.
3. **Parent container has no defined height or equal height to sticky item**: Sticky element has nowhere to travel.

**Stacking Context with `position`:**
Elements with `position: relative / absolute / fixed / sticky` and a `z-index` other than `auto` form a local stacking context. Children with `z-index: 9999` cannot break out of their parent's stacking context.

```css
/* Sticky Sidebar layout */
.main-wrapper {
  display: flex;
  align-items: flex-start; /* Ensures sidebar doesn't stretch to full container height */
}

.sticky-sidebar {
  position: sticky;
  top: 20px;
  width: 280px;
}
```
