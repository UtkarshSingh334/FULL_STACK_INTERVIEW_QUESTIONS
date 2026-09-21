# 🟢 Express.js - Medium & API Architecture

> **Topics Covered:** Express Middleware 5 Types, Centralized Error Handling, Request Validation (Zod / Joi), File Uploads with Multer, Pagination, Filtering, and Sorting Implementation, Rate Limiting, CORS Architecture, Helmet Security Headers, Preventing NoSQL Injection, Large App Folder Structure.

---

### Q1: The 5 Types of Express Middleware
**Question:** Explain the 5 different categories of middleware in Express with code examples.

**Answer:**
1. **Application-Level**: Bound to `app.use()` across the entire app.
2. **Router-Level**: Bound to an instance of `express.Router()`.
3. **Built-In**: `express.json()`, `express.urlencoded()`, `express.static()`.
4. **Third-Party**: `cors()`, `helmet()`, `morgan()`.
5. **Error-Handling**: Identified by **4 parameters** `(err, req, res, next)`.

---

### Q2: Centralized Global Error-Handling Middleware ⭐⭐
**Question:** How do you implement a centralized error handling class and middleware in Express?

**Answer:**

```javascript
// 1. Custom Error Class
class AppError extends Error {
  constructor(message, statusCode) {
    super(message);
    this.statusCode = statusCode;
    this.isOperational = true; // Distinguishes programmatic bugs from user errors
    Error.captureStackTrace(this, this.constructor);
  }
}

// 2. Global Error Middleware (Placed at very end of app.js)
const errorHandler = (err, req, res, next) => {
  err.statusCode = err.statusCode || 500;
  err.message = err.message || 'Internal Server Error';

  console.error(`[Error ${err.statusCode}]:`, err.message);

  res.status(err.statusCode).json({
    success: false,
    status: err.statusCode,
    message: err.message,
    ...(process.env.NODE_ENV === 'development' && { stack: err.stack }),
  });
};

module.exports = { AppError, errorHandler };
```

---

### Q3: Pagination, Filtering, and Sorting Implementation
**Question:** Write an Express route handler implementing pagination, field filtering, and sorting.

**Answer:**

```javascript
app.get('/api/products', async (req, res, next) => {
  try {
    // 1. Filtering
    const queryObj = { ...req.query };
    const excludedFields = ['page', 'sort', 'limit', 'fields'];
    excludedFields.forEach(el => delete queryObj[el]);

    // 2. Advanced filtering (e.g. price[gte]=100)
    let queryStr = JSON.stringify(queryObj);
    queryStr = queryStr.replace(/(gte|gt|lte|lt)/g, match => `$${match}`);
    let query = Product.find(JSON.parse(queryStr));

    // 3. Sorting
    if (req.query.sort) {
      const sortBy = req.query.sort.split(',').join(' ');
      query = query.sort(sortBy);
    } else {
      query = query.sort('-createdAt');
    }

    // 4. Pagination
    const page = parseInt(req.query.page, 10) || 1;
    const limit = parseInt(req.query.limit, 10) || 10;
    const skip = (page - 1) * limit;
    query = query.skip(skip).limit(limit);

    const products = await query;
    res.status(200).json({ success: true, count: products.length, page, data: products });
  } catch (err) {
    next(err);
  }
});
```

---

### Q4: Securing Express: CORS, Helmet, Rate Limiting & NoSQL Injection
**Question:** How do you harden an Express API against attacks?

**Answer:**
```javascript
const express = require('express');
const helmet = require('helmet');
const cors = require('cors');
const rateLimit = require('express-rate-limit');
const mongoSanitize = require('express-mongo-sanitize');

const app = express();

// 1. Helmet: Sets HTTP Security Headers (HSTS, X-Content-Type-Options, CSP)
app.use(helmet());

// 2. CORS: Restrict Allowed Origins
app.use(cors({
  origin: 'https://mytrustedfrontend.com',
  credentials: true,
}));

// 3. Rate Limiting: Prevent Brute-force & DDoS
const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100, // 100 requests per IP
  message: 'Too many requests from this IP, please try again later.',
});
app.use('/api', limiter);

// 4. Body Parser with limit
app.use(express.json({ limit: '10kb' }));

// 5. Data Sanitization against NoSQL query injection (strips $ and . characters)
app.use(mongoSanitize());
```

---

### Q5: Large Scale Production Express Folder Structure
**Question:** What is the recommended production folder architecture for a scalable Express project?

**Answer:**
```
src/
├── config/             # Environment variables & DB connection
│   ├── db.js
│   └── env.js
├── controllers/        # Request/Response orchestration logic
│   ├── authController.js
│   └── userController.js
├── middlewares/        # Custom middleware (auth, rateLimit, error)
│   ├── authMiddleware.js
│   └── errorMiddleware.js
├── models/             # Mongoose schemas / Database entities
│   └── User.js
├── routes/             # Express Router definitions
│   ├── authRoutes.js
│   └── userRoutes.js
├── services/           # Reusable business logic layer
│   └── userService.js
├── utils/              # Helper utilities, logger, custom error classes
│   ├── appError.js
│   └── logger.js
├── app.js              # Express app setup & middleware pipeline
└── server.js           # Server listen & process lifecycle events
```
