# 🎨 CSS - Easy Questions From Notes

> **Topics from Notes Covered:** Types of CSS (Inline, Internal, External, CSS Modules), CSS Position types (`static`, `relative`, `absolute`, `fixed`, `sticky`).

---

### Q1: Types of CSS
**Question (From Notes):** What are the different types of CSS (ways to apply styling), and how do they differ?

**Answer:**
1. **Inline CSS**: Defined directly on HTML elements using the `style` attribute.
   - *Example*: `<p style="color: blue; font-size: 16px;">Hello</p>`
   - *Pros/Cons*: Highest specificity (`1-0-0-0`), but difficult to maintain and lacks reusability.
2. **Internal CSS**: Defined inside `<style>` tags within the `<head>` section of an HTML document.
   - *Example*: `<style> p { color: blue; } </style>`
   - *Pros/Cons*: Scoped to single document; cannot be shared across multiple pages.
3. **External CSS**: Written in separate `.css` files and linked using `<link rel="stylesheet" href="styles.css">`.
   - *Pros/Cons*: Cached by browser across pages, clean separation of concerns. Industry standard.
4. **CSS Modules**: Component-scoped CSS where class names are hashed at build time (e.g., in React/Next.js).
   - *Example*: `import styles from './Button.module.css'; <button className={styles.btn}>`
   - *Pros/Cons*: Completely prevents class name collisions.

---

### Q2: Position in CSS (`static`, `relative`, `absolute`, `fixed`, `sticky`)
**Question (From Notes):** Explain all `position` values in CSS and how each alters document flow.

**Answer:**
1. **`static`** (Default): Follows normal document flow. `top`, `left`, `right`, `bottom`, and `z-index` have no effect.
2. **`relative`**: Stays in the normal document flow. Offsets relative to its *own default position* without affecting sibling elements. Acts as a reference container for absolute children.
3. **`absolute`**: Removed from the normal document flow. Positioned relative to the nearest **non-static ancestor** (`relative`, `absolute`, `fixed`, `sticky`).
4. **`fixed`**: Removed from normal flow. Positioned relative to the **viewport**. Does not scroll with the page.
5. **`sticky`**: Hybrid. Acts as `relative` until the viewport crosses a defined scroll threshold (e.g., `top: 0`), after which it sticks like `fixed` within its parent boundary.

```css
.card-container {
  position: relative; /* Anchor for absolute child */
  width: 300px;
  height: 200px;
}
.badge {
  position: absolute;
  top: 10px;
  right: 10px;
}
.navbar {
  position: sticky;
  top: 0;
}
```
