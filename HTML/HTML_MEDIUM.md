# 🌐 HTML - Medium Questions

> **Topics Covered:** Script Loading (`async` vs `defer` vs normal), Client-Side Storage (`localStorage` vs `sessionStorage` vs Cookies), HTML5 Form Validations, `target="_blank"` with `rel="noopener noreferrer"`, Audio & Video Tags, Iframe & Security, Meta Viewport & Responsive Meta Tags, Data Attributes (`data-*`), SVG vs Canvas.

---

### Q1: Script Loading: Regular vs `async` vs `defer`
**Question:** Explain how `<script>`, `<script async>`, and `<script defer>` differ during HTML parsing.

**Answer:**
- **Regular `<script>`**: Parsing of HTML stops immediately. The script is fetched and executed before HTML parsing resumes. Blocks DOM rendering.
- **`<script async>`**: Script is fetched asynchronously in parallel with HTML parsing. As soon as the script finishes downloading, HTML parsing pauses to execute the script. Execution order is non-deterministic (scripts run in order of download speed).
- **`<script defer>`**: Script is fetched in parallel with HTML parsing, but execution is deferred until the HTML document has been fully parsed (right before `DOMContentLoaded`). Preserves execution order.

```html
<!-- Independent analytics / tracking tag -->
<script async src="analytics.js"></script>

<!-- Script dependent on DOM elements / jQuery / React bundle -->
<script defer src="app.js"></script>
```

---

### Q2: Client Storage: `localStorage` vs `sessionStorage` vs `Cookies`
**Question:** Compare `localStorage`, `sessionStorage`, and `Cookies` in detail.

**Answer:**
| Feature | `localStorage` | `sessionStorage` | Cookies (`document.cookie`) |
| :--- | :--- | :--- | :--- |
| **Capacity** | ~5 MB - 10 MB | ~5 MB | ~4 KB |
| **Expiration** | Persistent until explicitly deleted | Expires when browser tab is closed | Configurable via `Expires` / `Max-Age` |
| **Server Transfer** | Never sent automatically with HTTP requests | Never sent automatically | Automatically sent in HTTP request headers |
| **Scope** | Same Origin (all tabs/windows) | Same Origin & Same Tab | Same Origin (Domain & Path) |
| **Security Flags**| Accessible via JS (XSS target) | Accessible via JS | Supports `HttpOnly`, `Secure`, `SameSite` |

```javascript
// LocalStorage
localStorage.setItem("token", "abc123xyz");
const token = localStorage.getItem("token");
localStorage.removeItem("token");

// SessionStorage
sessionStorage.setItem("sessionId", "session_99");

// Cookie (secure setup)
document.cookie = "user=Utkarsh; SameSite=Strict; Secure; max-age=3600";
```

---

### Q3: HTML5 Native Form Validations & Input Types
**Question:** What native validation attributes and new input types were introduced in HTML5?

**Answer:**
- **HTML5 Input Types:** `email`, `number`, `tel`, `url`, `date`, `time`, `color`, `range`, `file`.
- **Validation Attributes:**
  - `required`: Prevents submission if field is empty.
  - `pattern`: Regex pattern that input value must match.
  - `min` / `max`: Boundary constraints for numbers and dates.
  - `minlength` / `maxlength`: String length constraints.
  - `step`: Legal number intervals.

```html
<form>
  <input type="email" placeholder="Email" required>
  <input type="text" pattern="[A-Z]{5}[0-9]{4}[A-Z]{1}" placeholder="PAN Number">
  <input type="number" min="18" max="100" required>
  <button type="submit">Submit</button>
</form>
```

---

### Q4: Security: `target="_blank"` and `rel="noopener noreferrer"`
**Question:** Why must you always add `rel="noopener noreferrer"` when opening links with `target="_blank"`?

**Answer:**
- **The Reverse Tabnabbing Security Risk:**
  When a user clicks a link with `target="_blank"`, the newly opened page gains access to the originating window's `window.opener` object. The target page can execute:
  `window.opener.location = "https://phishing-fake-login.com";`
- **Mitigation:**
  - `noopener`: Prevents `window.opener` from being populated in the new window (isolates processes).
  - `noreferrer`: Prevents sending the HTTP `Referer` header to the target site.

```html
<!-- Secure external hyperlink -->
<a href="https://external-bank.com" target="_blank" rel="noopener noreferrer">
  External Secure Portal
</a>
```

---

### Q5: Custom Data Attributes (`data-*`)
**Question:** What are `data-*` attributes and how do you access them in JavaScript and CSS?

**Answer:**
- Custom attributes allowing developers to store extra application data directly on HTML elements without affecting rendering.

```html
<button id="user-btn" data-user-id="4082" data-role="admin">User Profile</button>
```

```javascript
// Access in JavaScript
const btn = document.getElementById("user-btn");
console.log(btn.dataset.userId); // "4082"
console.log(btn.dataset.role);   // "admin"
```

```css
/* Access in CSS */
button[data-role="admin"] {
  border: 2px solid crimson;
}
```

---

### Q6: HTML5 Media: `<audio>` and `<video>`
**Question:** How do you implement native HTML5 audio and video players with fallbacks?

**Answer:**
```html
<video width="640" height="360" controls poster="thumbnail.jpg" preload="metadata">
  <source src="movie.mp4" type="video/mp4">
  <source src="movie.webm" type="video/webm">
  <p>Your browser does not support HTML5 video.</p>
</video>
```
- `controls`: Displays default browser play/pause/volume controls.
- `poster`: Image displayed before video plays.
- `preload`: `auto` | `metadata` | `none`.
