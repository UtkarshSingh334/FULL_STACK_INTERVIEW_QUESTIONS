# 🟢 Node.js & Express - Easy Questions

> **Topics Covered:** What is Node.js, V8 Engine & Libuv, Single-Threaded Non-Blocking Architecture, Node Modules (CommonJS vs ESM), What is Express.js, Basic Express Routing, `req.params` vs `req.query` vs `req.body`, HTTP Status Codes.

---

### Q1: What is Node.js and How Does It Work?
**Question:** What is Node.js? Why is it described as single-threaded and non-blocking?

**Answer:**
- **Node.js** is an open-source, cross-platform JavaScript runtime environment built on Chrome's **V8 JavaScript Engine**.
- **Architecture:**
  1. **Single-Threaded Event Loop**: Handles all client requests on a single main thread without allocating a new operating system thread per connection.
  2. **Non-Blocking Asynchronous I/O**: Offloads heavy I/O operations (file system, database queries, network requests) to **Libuv's C++ Threadpool** in the background.
  3. **High Concurrency**: Can handle tens of thousands of concurrent I/O-bound connections with minimal RAM overhead.

---

### Q2: CommonJS (`require`) vs ES Modules (`import`)
**Question:** Compare CommonJS and ES Modules in Node.js.

**Answer:**
| Feature | CommonJS (CJS) | ES Modules (ESM) |
| :--- | :--- | :--- |
| **Syntax** | `const fs = require('fs');` <br> `module.exports = { ... };` | `import fs from 'fs';` <br> `export default { ... };` |
| **Loading Model** | Synchronous loading at runtime | Asynchronous parsing and tree-shaking at compile time |
| **Top-Level `await`**| Not supported natively | Fully supported |
| **Node.js Default**| Default for standard `.js` | Enabled with `"type": "module"` in `package.json` or `.mjs` extension |

---

### Q3: What is Express.js and Basic Routing?
**Question:** What is Express.js? Create a basic Express HTTP server with GET and POST routes.

**Answer:**
- **Express.js** is a fast, unopinionated, minimalist web framework for Node.js providing routing, middleware integration, and HTTP utility methods.

```javascript
const express = require('express');
const app = express();

// Built-in middleware to parse JSON bodies
app.use(express.json());

// GET Route
app.get('/api/users', (req, res) => {
  res.status(200).json([{ id: 1, name: 'Utkarsh Singh' }]);
});

// POST Route
app.post('/api/users', (req, res) => {
  const newUser = req.body;
  res.status(201).json({ message: 'User created', data: newUser });
});

app.listen(3000, () => console.log('Server running on port 3000'));
```

---

### Q4: `req.params` vs `req.query` vs `req.body`
**Question:** What is the difference between `req.params`, `req.query`, and `req.body` in Express?

**Answer:**
1. **`req.params` (Route Parameters)**:
   Named URL path segments defined with `:` (e.g., `/users/:id` $ightarrow$ `/users/42` $ightarrow$ `req.params.id === "42"`).
2. **`req.query` (Query Parameters)**:
   Key-value pairs appended after `?` in the URL (e.g., `/users?role=admin&page=2` $ightarrow$ `req.query === { role: 'admin', page: '2' }`).
3. **`req.body` (Request Body Payload)**:
   Data sent in the HTTP POST/PUT/PATCH request body (parsed by `express.json()`).
