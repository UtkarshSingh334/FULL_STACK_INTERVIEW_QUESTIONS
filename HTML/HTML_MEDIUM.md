# 🌐 HTML - Medium Questions From Notes

> **Topics from Notes Covered:** `<script>` Tag Loading (Regular vs `async` vs `defer`), `href` vs `src`, GET vs POST in Forms.

---

### Q1: `<script>` Tag Loading: Regular vs `async` vs `defer`
**Question (From Notes):** How does the `<script>` tag work with `async` and `defer`?

**Answer:**
```
Regular:   HTML Parsing ===[PAUSE / Fetch & Exec Script]====> HTML Parsing Continues
Async:     HTML Parsing =======[Fetch Script in Parallel]====[PAUSE / Exec Script]==> HTML Parsing Continues
Defer:     HTML Parsing ======================================> [Exec Script after parsing completes]
```

1. **Regular `<script src="...">`**: HTML parsing pauses while the script downloads and executes immediately.
2. **`<script async src="...">`**: Script downloads in background. As soon as download finishes, HTML parsing pauses while the script executes. Execution order is non-deterministic (whichever finishes downloading first executes first). Ideal for independent scripts (e.g., analytics).
3. **`<script defer src="...">`**: Script downloads in background. Executes only after the entire HTML document is parsed (just before `DOMContentLoaded`), in the exact written order in HTML. Ideal for scripts dependent on DOM or other scripts.

---

### Q2: `href` vs `src` Attributes
**Question (From Notes):** What is the difference between `href` and `src`?

**Answer:**
- **`href` (Hypertext Reference)**: Specifies the location of a web resource to establish a link/relationship. It is **non-blocking** (the browser downloads it in the background without halting document parsing).
  - *Examples*: `<link rel="stylesheet" href="style.css">`, `<a href="page.html">`
- **`src` (Source)**: Points to an external resource that is **downloaded and embedded directly into the document**. It is **blocking** by default during parsing.
  - *Examples*: `<script src="app.js">`, `<img src="pic.jpg">`, `<iframe src="...">`

---

### Q3: GET and POST in Forms
**Question (From Notes):** Compare GET and POST methods in HTML `<form>` submissions.

**Answer:**
| Feature | `<form method="GET">` | `<form method="POST">` |
| :--- | :--- | :--- |
| **Data Transmission** | Appended to URL query string (`/search?query=val`) | Sent inside HTTP request payload body |
| **Size Limit** | Limited by maximum URL length (~2048 characters) | No strict limit (set on web server) |
| **Caching & History** | URL cached in browser history and bookmarkable | Not cached or saved in browser history |
| **Security** | Sensitive data exposed in URL logs | Safer for sensitive data (encrypted in body over HTTPS) |
| **Idempotency** | Idempotent (safe to re-run for search queries) | Non-idempotent (re-submitting can create duplicate records) |

```html
<!-- GET Form -->
<form action="/search" method="GET">
  <input type="text" name="keyword" placeholder="Search..." />
  <button type="submit">Search</button>
</form>

<!-- POST Form -->
<form action="/register" method="POST">
  <input type="password" name="password" />
  <button type="submit">Register</button>
</form>
```
