# 🌐 HTML - Hard Questions From Notes

> **Topics from Notes Covered:** In-depth `<script>` loading parser internals, Semantic Accessibility Tree parsing, Form Encoding Types (`application/x-www-form-urlencoded` vs `multipart/form-data`).

---

### Q1: Script Loading Parser Internals: Performance Impact of `async` vs `defer`
**Question (From Notes):** How does the browser HTML parser handle script tags with `async`, `defer`, and dynamic script injection under the hood?

**Answer:**
- When the HTML tokenizer encounters a regular `<script>`, it halts DOM tree construction (parser-blocking) until network download finishes and JS executes.
- With `async`, the parser continues tokenizing while the download occurs on a secondary network thread. As soon as the script bytes arrive, the HTML parser pauses, executes the script, and resumes parsing.
- With `defer`, scripts download in parallel and are queued. The browser executes them sequentially right before firing the `DOMContentLoaded` event, guaranteeing DOM availability without blocking the initial paint.

---

### Q2: Form Submission Encodings: `GET` vs `POST` (`urlencoded` vs `multipart/form-data`)
**Question (From Notes):** How are form data payloads formatted during GET vs POST submissions?

**Answer:**
1. **GET**: The browser serializes key-value pairs using percent-encoding into the URL query string: `name=Utkarsh&role=Dev`.
2. **POST (`application/x-www-form-urlencoded`)**: Key-value pairs are formatted identically to query strings but placed in the HTTP body.
3. **POST (`multipart/form-data`)**: Required when uploading files (`<input type="file">`). Each field is enclosed within boundary delimiters with its own `Content-Disposition` and `Content-Type`.

```html
<form action="/upload-profile" method="POST" enctype="multipart/form-data">
  <input type="text" name="username" value="Utkarsh" />
  <input type="file" name="avatar" />
  <button type="submit">Submit</button>
</form>
```
