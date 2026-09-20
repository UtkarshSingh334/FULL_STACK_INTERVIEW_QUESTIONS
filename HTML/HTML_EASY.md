# 🌐 HTML - Questions From Notes

> **Topics from Notes Covered:** HTML vs HTML5, Semantic vs Non-Semantic Tags, Block vs Inline Tags, Why use HTML, `<script>` Tag (Regular vs `async` vs `defer`), `href` vs `src`, GET vs POST in Forms.

---

### Q1: HTML vs HTML5
**Question (From Notes):** What are the core differences between HTML and HTML5? Why do we use HTML5?

**Answer:**
- **HTML (HTML4)**: Older standard relying on generic `<div>` containers with classes, required third-party plugins (Flash) for audio/video, and lacked native storage.
- **HTML5**: Modern web standard providing native semantic layout elements (`<header>`, `<nav>`, `<article>`, `<section>`, `<footer>`), native multimedia (`<audio>`, `<video>`), and client storage (`localStorage`, `sessionStorage`).

```html
<!-- HTML4 -->
<div id="header"><div class="nav">...</div></div>

<!-- HTML5 Semantic -->
<header>
  <nav>
    <ul><li><a href="#home">Home</a></li></ul>
  </nav>
</header>
<main>
  <article>
    <h1>HTML5 Web Standard</h1>
    <p>Semantic tags improve accessibility and SEO.</p>
  </article>
</main>
<footer><p>&copy; 2026</p></footer>
```

---

### Q2: Semantic Tags vs Non-Semantic Tags
**Question (From Notes):** What are semantic tags with examples, and what are non-semantic tags?

**Answer:**
- **Semantic Tags**: Clearly describe their meaning and purpose to the browser and developer (e.g., `<header>`, `<nav>`, `<main>`, `<article>`, `<section>`, `<aside>`, `<footer>`, `<figure>`).
  - *Benefits*: Better SEO, accessibility for screen readers (a11y), and readable code structure.
- **Non-Semantic Tags**: Tell nothing about their content (e.g., `<div>` and `<span>`).

```html
<!-- Non-Semantic (Generic containers) -->
<div class="menu">
  <span class="menu-item">Home</span>
</div>

<!-- Semantic (Meaningful structure) -->
<nav aria-label="Main Menu">
  <a href="/home">Home</a>
</nav>
```

---

### Q3: Block vs Inline vs Inline-Block Elements
**Question (From Notes):** Differentiate between Block and Inline tags with examples.

**Answer:**
| Property | Block Tags | Inline Tags | Inline-Block Tags |
| :--- | :--- | :--- | :--- |
| **New Line** | Always starts on a new line; occupies 100% width | Flows on the same line | Flows on the same line |
| **Width & Height** | Fully customizable (`width: 300px;`) | Cannot be set (derived from content) | Fully customizable |
| **Margin / Padding** | Top, bottom, left, right all apply | Left and right only (vertical does not push siblings) | Top, bottom, left, right all apply |
| **Examples** | `<div>`, `<p>`, `<h1>`-`<h6>`, `<section>`, `<form>` | `<span>`, `<a>`, `<strong>`, `<em>`, `<code>` | `<button>`, `<input>`, `<img>` |

---

### Q4: Why use HTML?
**Question (From Notes):** Why do we use HTML in web development?

**Answer:**
1. **Structural Skeleton**: HTML provides the fundamental building blocks and hierarchy for all web pages.
2. **Universal Browser Compatibility**: Interpreted natively by every web browser across all operating systems and mobile devices.
3. **Hyperlinking & Web Webbing**: Anchors (`<a href="...">`) interconnect documents globally.
4. **Accessibility & Assistive Tech**: Provides standardized semantic landmarks for screen readers and search engines.
