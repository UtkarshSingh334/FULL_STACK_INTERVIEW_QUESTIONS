# 🟢 Node.js & Express - Medium Questions

> **Topics Covered:** Express Middleware Architecture (Application, Router, Error-Handling, Third-Party), Authentication with JWT & Password Hashing with Bcrypt, RESTful API Standards & Status Codes, Error-Handling Middleware, CORS & Security Headers (Helmet).

---

### Q1: Express Middleware Architecture ⭐⭐
**Question:** What is middleware in Express? Explain the different types of middleware and write a custom logger and auth middleware.

**Answer:**
Middleware functions are functions that have access to the Request object (`req`), Response object (`res`), and the `next` middleware function in the application's request-response cycle.

#### Types of Middleware:
1. **Application-level**: `app.use((req, res, next) => { ... })`
2. **Router-level**: `router.use('/admin', authMiddleware)`
3. **Built-in**: `express.json()`, `express.static('public')`
4. **Third-party**: `cors()`, `morgan()`, `helmet()`
5. **Error-handling**: Middleware taking 4 parameters: `(err, req, res, next)`

```javascript
// Custom Logging Middleware
const logger = (req, res, next) => {
  console.log(`[${new Date().toISOString()}] ${req.method} ${req.originalUrl}`);
  next(); // Pass execution to next middleware
};

// Custom Auth Middleware
const requireAuth = (req, res, next) => {
  const token = req.headers.authorization?.split(' ')[1];
  if (!token) {
    return res.status(401).json({ error: 'Unauthorized: No token provided' });
  }
  // verify token...
  req.userId = 101;
  next();
};

app.use(logger);
app.get('/api/protected', requireAuth, (req, res) => {
  res.json({ message: 'Secret data', userId: req.userId });
});
```

---

### Q2: Authentication with JWT (JSON Web Tokens) & Bcrypt
**Question:** Explain how JWT authentication and bcrypt password hashing work in a Node/Express backend.

**Answer:**
1. **Password Hashing (Bcrypt)**:
   - When registering, pass user password through `bcrypt.hash(password, 10)` with salted hashing.
   - On login, compare plain password with stored hash via `bcrypt.compare()`.
2. **JWT Flow**:
   - JWT contains 3 base64 encoded parts: `Header.Payload.Signature`.
   - On valid login, server signs payload with secret key (`jwt.sign()`) and returns token to client.
   - Client stores token and sends it in `Authorization: Bearer <token>` header for protected routes.

```javascript
const jwt = require('jsonwebtoken');
const bcrypt = require('bcryptjs');

// Register: Hash password
const hashedPassword = await bcrypt.hash('mySecretPassword', 10);

// Login: Verify & Generate JWT
const isMatch = await bcrypt.compare('mySecretPassword', hashedPassword);
if (isMatch) {
  const token = jwt.sign({ userId: 101, role: 'admin' }, process.env.JWT_SECRET, { expiresIn: '1h' });
  res.json({ token });
}
```

---

### Q3: Global Error-Handling Middleware in Express
**Question:** How do you implement centralized error handling in Express?

**Answer:**
```javascript
// 4-argument error handling middleware placed at the VERY END of app.js
app.use((err, req, res, next) => {
  const statusCode = err.statusCode || 500;
  console.error('[Error Occurred]:', err.stack);

  res.status(statusCode).json({
    success: false,
    message: err.message || 'Internal Server Error',
    ...(process.env.NODE_ENV === 'development' && { stack: err.stack }),
  });
});
```
