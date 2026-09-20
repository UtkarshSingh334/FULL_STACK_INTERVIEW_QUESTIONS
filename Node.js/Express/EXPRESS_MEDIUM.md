# 🟢 Express & Node.js - Medium Questions From Notes

> **Topics from Notes Covered:** Middleware Types & BATER Mnemonic, JWT Workflow, Why Only Bcrypt is Used for Password Hashing vs SHA-256, Rate Limiting (`ratelimiting`), CORS in Express.

---

### Q1: Express Middleware & The BATER Types
**Question (From Notes):** What is Express middleware? Explain the BATER types of middleware.

**Answer:**
Middleware functions have access to `req`, `res`, and `next()`.

**BATER Types:**
1. **B - Built-in**: Ships with Express (e.g. `express.json()`, `express.urlencoded()`, `express.static()`).
2. **A - Application-level**: Attached to `app.use()` (e.g. logging, authentication).
3. **T - Third-party**: Installed from npm (e.g. `cors()`, `helmet()`, `morgan()`).
4. **E - Error-handling**: Defined with **4 arguments** `(err, req, res, next)`.
5. **R - Router-level**: Attached to an `express.Router()` instance.

```javascript
const express = require('express');
const app = express();
const router = express.Router();

// 1. Built-in
app.use(express.json());

// 2. Application-level
app.use((req, res, next) => {
  console.log(`${req.method} ${req.url}`);
  next();
});

// 3. Router-level
router.use((req, res, next) => {
  if (!req.headers.authorization) return next(new Error("Unauthorized"));
  next();
});
router.get('/dashboard', (req, res) => res.send("Secure Dashboard"));
app.use('/api', router);

// 4. Error-handling (Must have 4 parameters)
app.use((err, req, res, next) => {
  console.error("Error:", err.message);
  res.status(500).json({ error: true, message: err.message });
});
```

---

### Q2: JWT (JSON Web Token) Workflow
**Question (From Notes):** Explain the JWT structure and authentication workflow.

**Answer:**
A JWT has 3 parts: `Header.Payload.Signature`.
- **Header**: Algorithm & token type.
- **Payload**: Claims (e.g., `userId`, `role`, expiration `exp`).
- **Signature**: `HMACSHA256(base64Url(header) + "." + base64Url(payload), secretKey)` to prevent tampering.

**Workflow:**
1. Client logs in with email & password.
2. Server validates credentials and returns a short-lived **Access Token** (15m) + a secure **Refresh Token** (7d in `HttpOnly` cookie).
3. Client sends Access Token in `Authorization: Bearer <token>` header for subsequent requests.
4. When Access Token expires (`401`), client hits `/refresh-token` with the Refresh Token to obtain a new Access Token.

---

### Q3: Why Only `bcrypt` is Used for Password Hashing (vs SHA-256)
**Question (From Notes):** Why is only `bcrypt` recommended for password hashing instead of fast hashing algorithms like SHA-256?

**Answer:**
1. **Speed Vulnerability**: SHA-256 is designed to be extremely fast for file checksums. Modern GPUs can calculate billions of SHA-256 hashes per second, making brute-force dictionary attacks trivial.
2. **Work Factor / Adaptive Cost**: `bcrypt` has a configurable cost factor (`saltRounds`, e.g. 12). As computing hardware speeds up, the cost factor can be increased to make hashing intentionally computationally expensive.
3. **Automatic Salt Generation**: `bcrypt` automatically generates and embeds a random 128-bit salt inside the output hash, completely defeating Rainbow Table attacks.

```javascript
const bcrypt = require('bcrypt');

async function hashPassword(plainText) {
  const salt = await bcrypt.genSalt(12);
  return await bcrypt.hash(plainText, salt);
}

async function verifyPassword(plainText, hashedPassword) {
  return await bcrypt.compare(plainText, hashedPassword);
}
```

---

### Q4: Rate Limiting (`ratelimiting`)
**Question (From Notes):** What is rate limiting and how is it implemented?

**Answer:**
Rate limiting restricts the number of requests a client can make in a specified time window to prevent brute-force attacks and Denial-of-Service (DoS).

```javascript
const rateLimit = require('express-rate-limit');

const loginLimiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 5, // Limit 5 login attempts per IP per 15 minutes
  message: { error: "Too many login attempts. Try again in 15 minutes." }
});

app.post('/api/login', loginLimiter, (req, res) => {
  // Login handler
});
```

---

### Q5: CORS (Cross-Origin Resource Sharing) in Express
**Question (From Notes):** How do you configure CORS in an Express app?

```javascript
const cors = require('cors');

app.use(cors({
  origin: ['http://localhost:3000', 'https://myapp.com'],
  methods: ['GET', 'POST', 'PUT', 'DELETE'],
  credentials: true
}));
```
