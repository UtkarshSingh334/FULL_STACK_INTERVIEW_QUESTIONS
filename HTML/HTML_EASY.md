# 🌐 HTML - Easy Questions

> **Topics Covered:** HTML vs HTML5, Semantic vs Non-Semantic Tags, Block vs Inline Elements, Why use HTML, `<script>` Tag (`async` vs `defer`), `href` vs `src`, `id` vs `class`, `alt` attribute, GET vs POST in Forms, HTML Document Structure & Doctype, Lists (`<ul>`, `<ol>`, `<dl>`), Forms & Common Inputs.

---

### Q1: What is HTML and why do we use it?
**Question:** What is HTML? Why do we use HTML in web development?

**Answer:**
- **HTML (HyperText Markup Language)** is the standard markup language used to create the structural skeleton of web pages.
- **Why use HTML:**
  1. **Structural Skeleton**: Defines headings, paragraphs, links, images, tables, forms, and media.
  2. **Universal Compatibility**: Understood and rendered natively by all web browsers across devices.
  3. **Hyperlinking**: Connects documents across the web via hyperlinks (`<a>`).
  4. **Accessibility & SEO**: Enables screen readers and search engine web crawlers to interpret page content.

---

### Q2: HTML vs HTML5
**Question:** What are the key differences between HTML (HTML4) and HTML5?

**Answer:**
| Feature | HTML4 | HTML5 |
| :--- | :--- | :--- |
| **Doctype** | Long and complex SGML declaration | Simple: `<!DOCTYPE html>` |
| **Semantic Elements** | Generic `<div>` and `<span>` tags | `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>` |
| **Media Support** | Required Flash / Silverlight plugins | Native `<audio>` and `<video>` tags |
| **Client-Side Storage** | Relied primarily on cookies (4KB limit) | Native `localStorage` and `sessionStorage` (5-10MB) |
| **Graphics** | Limited | Native `<canvas>` (2D/3D) and `<svg>` support |
| **Mobile & Device APIs** | Poor mobile support | Geolocation, Web Workers, Device Orientation APIs |

```html
<!-- HTML5 Standard Structure -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>HTML5 Web App</title>
</head>
<body>
  <header>
    <nav><ul><li><a href="#home">Home</a></li></ul></nav>
  </header>
  <main>
    <article>
      <h1>Semantic Web</h1>
      <p>Clean structure for a11y and SEO.</p>
    </article>
  </main>
  <footer><p>&copy; 2026</p></footer>
</body>
</html>
```

---

### Q3: Semantic Tags vs Non-Semantic Tags
**Question:** What are semantic tags with examples, and what are non-semantic tags? Why are semantic tags important?

**Answer:**
- **Semantic Tags**: Elements whose tag names describe their meaning to both the browser and developer (e.g., `<header>`, `<nav>`, `<main>`, `<article>`, `<section>`, `<aside>`, `<footer>`, `<figure>`, `<mark>`).
- **Non-Semantic Tags**: Elements that give zero indication about their content (e.g., `<div>`, `<span>`).
- **Why Semantic Tags Matter:**
  1. **SEO (Search Engine Optimization)**: Search engine crawlers understand content hierarchy better.
  2. **Accessibility (a11y)**: Screen readers use semantic landmarks for voice navigation.
  3. **Maintainability**: Clean and self-describing code for development teams.

---

### Q4: Block vs Inline vs Inline-Block Elements
**Question:** Differentiate between Block, Inline, and Inline-Block elements with examples.

**Answer:**
| Property | Block Elements | Inline Elements | Inline-Block Elements |
| :--- | :--- | :--- | :--- |
| **Line Flow** | Starts on a new line; takes 100% available width | Continues on the same line | Continues on the same line |
| **Width & Height** | Customizable (`width: 200px; height: 100px;`) | Cannot be set directly | Customizable |
| **Margins & Padding** | Top, bottom, left, right all apply | Left/right apply; vertical does not push surrounding content | Top, bottom, left, right all apply |
| **Examples** | `<div>`, `<p>`, `<h1>`-`<h6>`, `<section>`, `<form>`, `<ul>` | `<span>`, `<a>`, `<strong>`, `<em>`, `<code>` | `<button>`, `<input>`, `<img>`, `<select>` |

---

### Q5: `id` vs `class` Attributes
**Question:** What is the difference between `id` and `class` attributes in HTML?

**Answer:**
- **`id` Attribute:**
  - Must be **unique** within the entire HTML document.
  - Used for targeted JavaScript manipulation (`document.getElementById`) and fragment URL navigation (`#section-id`).
  - Highest CSS selector specificity among basic selectors (`#my-id`).
- **`class` Attribute:**
  - Can be shared across **multiple** elements in the same page.
  - An element can have multiple space-separated classes (e.g., `class="btn btn-primary active"`).
  - Used for reusable CSS styling and grouping elements in JavaScript (`querySelectorAll`).

---

### Q6: `href` vs `src`
**Question:** What is the difference between `href` and `src` attributes?

**Answer:**
- **`href` (Hypertext Reference)**:
  - Specifies the location of an external resource that is **linked** to the current document.
  - Browser does not block rendering while downloading the linked resource (e.g., `<a href="...">`, `<link rel="stylesheet" href="...">`).
- **`src` (Source)**:
  - Specifies the external resource that is to be **embedded/downloaded and executed** in place of the tag.
  - Browser pauses parsing until the resource is fetched and loaded (e.g., `<img src="...">`, `<script src="...">`, `<iframe src="...">`).

---

### Q7: Purpose of the `alt` Attribute in `<img>`
**Question:** Why is the `alt` attribute important in `<img>` tags?

**Answer:**
1. **Accessibility (a11y)**: Screen readers read the alt text aloud for visually impaired users.
2. **Fallback Content**: Displayed in place of the image if the image link is broken or the network fails.
3. **SEO Ranking**: Helps search engine bots index the image and understand page topic context.

```html
<img src="profile.jpg" alt="Profile photo of Utkarsh Singh">
```

---

### Q8: Form Submission: GET vs POST Methods
**Question:** What is the difference between GET and POST form submission methods?

**Answer:**
| Criteria | GET Method | POST Method |
| :--- | :--- | :--- |
| **Data Transmission** | Appended to URL as query parameters (`?name=value`) | Sent securely in the HTTP Request Body |
| **Data Visibility** | Visible in URL and browser history | Hidden from URL address bar |
| **Data Length Limit** | Restricted by URL length limits (~2048 chars) | No fixed limit; can send large payloads & files |
| **Caching & Bookmarking**| Can be cached, bookmarked, and reloaded | Cannot be bookmarked; reloading prompts re-submit |
| **Primary Use Case** | Fetching/filtering data (Search, Read) | Modifying data / sensitive actions (Login, Upload) |

```html
<!-- GET Form -->
<form action="/search" method="GET">
  <input type="text" name="query" placeholder="Search...">
  <button type="submit">Search</button>
</form>

<!-- POST Form -->
<form action="/login" method="POST">
  <input type="email" name="email" required>
  <input type="password" name="password" required>
  <button type="submit">Login</button>
</form>
```

---

### Q9: What is `<!DOCTYPE html>`?
**Question:** What is the purpose of `<!DOCTYPE html>` declaration?

**Answer:**
- It is an instruction to the web browser about the version of HTML the page is written in.
- In HTML5, `<!DOCTYPE html>` ensures the browser renders the page in **Standards Mode** rather than Quirks Mode (which emulated legacy bugs from older browsers).

---

### Q10: HTML Lists: `<ul>`, `<ol>`, `<dl>`
**Question:** What are the types of lists in HTML?

**Answer:**
1. **Unordered List (`<ul>`)**: Bulleted list of items (`<li>`).
2. **Ordered List (`<ol>`)**: Numbered or lettered list of items (`<li>`).
3. **Description List (`<dl>`)**: List of terms (`<dt>`) and descriptions (`<dd>`).

```html
<dl>
  <dt>HTML</dt>
  <dd>HyperText Markup Language</dd>
  <dt>CSS</dt>
  <dd>Cascading Style Sheets</dd>
</dl>
```
