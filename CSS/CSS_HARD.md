# 🎨 CSS - Advanced / Hard Questions

> **Topics Covered:** CSS Performance & GPU Acceleration (`transform`, `opacity`, `will-change`), BEM Methodology & CSS Architecture, CSS Variables / Custom Properties, CSS Subgrid, Container Queries (`@container`), Advanced Transitions vs Keyframe Animations, Reflow vs Repaint.

---

### Q1: Browser Rendering Performance: Reflow vs Repaint vs Composite
**Question:** Explain Reflow (Layout), Repaint, and Composite in CSS. Which CSS properties trigger GPU acceleration?

**Answer:**
- **Reflow (Layout Thrashing)**: Recalculates the geometry and positions of elements on the page. Extremely costly.
  - *Triggered by:* `width`, `height`, `margin`, `padding`, `display`, `top`, `left`, `fontSize`, `offsetWidth`.
- **Repaint**: Visual changes that do not affect geometry.
  - *Triggered by:* `color`, `background-color`, `border-color`, `box-shadow`, `visibility`.
- **Composite (GPU Acceleration)**: Layers are combined by the GPU on a separate compositor thread without touching the main CPU thread.
  - *Triggered by:* `transform` (`translate3d`, `scale`), `opacity`, `filter`.

```css
/* High Performance Animation (60 FPS) */
.animated-card {
  will-change: transform, opacity;
  transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1), opacity 0.3s ease;
}
.animated-card:hover {
  transform: translateY(-8px) scale(1.02);
}
```

---

### Q2: CSS Custom Properties (Variables) vs Preprocessor Variables (Sass)
**Question:** How do CSS Custom Properties (`--var`) differ from Sass/SCSS variables (`$var`)?

**Answer:**
- **CSS Custom Properties:**
  - Resolved **at runtime** in the browser DOM.
  - Fully dynamic; inherit down the DOM tree and can be updated via JavaScript (`element.style.setProperty()`) or media queries.
  - Perfect for theme switching (Dark mode / Light mode).
- **Sass Variables:**
  - Compiled **at build time** into static CSS values. No runtime DOM awareness.

```css
:root {
  --bg-color: #ffffff;
  --text-color: #1a1a1a;
}
[data-theme="dark"] {
  --bg-color: #121212;
  --text-color: #f5f5f5;
}
body {
  background-color: var(--bg-color);
  color: var(--text-color);
  transition: background-color 0.3s;
}
```

---

### Q3: CSS Container Queries (`@container`) vs Media Queries (`@media`)
**Question:** What problem do CSS Container Queries solve?

**Answer:**
- Media queries adapt styling based on the **entire viewport width**.
- Container queries adapt a component's styling based on the **width of its direct parent container**, allowing truly modular, reusable components that work regardless of whether placed in a full-width hero section or a narrow 300px sidebar.

```css
.card-container {
  container-type: inline-size;
}

@container (min-width: 450px) {
  .card {
    display: flex;
    flex-direction: row;
  }
}
```
