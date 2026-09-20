# 🟢 Express & Node.js - Easy Questions From Notes

> **Topics from Notes Covered:** Node.js Relationship & Modules (Core, Local, Third-Party), Why `express.json()` is used.

---

### Q1: Node.js Relationship & Module System (Core, Local, Third-Party)
**Question (From Notes):** What is the relationship between Node.js, V8, and Libuv? Explain the Node.js module types.

**Answer:**
**Node.js Relationship Architecture:**
- **Chrome V8 Engine**: Compiles and executes JavaScript code.
- **Libuv**: C library that provides the Event Loop and asynchronous I/O (file system, network, thread pool).
- **Node.js Core APIs**: JavaScript wrapper bindings providing APIs (`fs`, `http`, `crypto`, `path`).

**3 Types of Modules:**
1. **Core Modules**: Built into Node binary (`require('fs')`, `require('path')`, `require('http')`).
2. **Local Modules**: User-created files (`require('./services/userService')`).
3. **Third-Party Modules**: Installed via npm into `node_modules` (`require('express')`, `require('bcrypt')`).

---

### Q2: Why is `express.json()` used?
**Question (From Notes):** Why do we need `express.json()` middleware in an Express application?

**Answer:**
Incoming HTTP requests transmit data as raw binary streams (`Buffer` chunks). By default, Express does not parse incoming request bodies, leaving `req.body` as `undefined`. `express.json()` listens to incoming data chunks, parses the JSON payload string, and attaches the resulting JavaScript object to `req.body`.

```javascript
const express = require('express');
const app = express();

// Required to parse application/json payloads
app.use(express.json());

app.post('/api/users', (req, res) => {
  console.log(req.body); // { name: "Utkarsh", email: "u@example.com" }
  res.status(201).json({ success: true, data: req.body });
});
```
