# 🟢 Express.js - Easy & Routing Fundamentals

> **Topics Covered:** What is Express.js & Why use it with Node?, Middleware Definition & `next()`, `app.use()` vs `app.get()`, Route Parameters vs Query Parameters vs Body, HTTP Methods (GET, POST, PUT, PATCH, DELETE), HTTP Status Codes (200, 201, 400, 401, 403, 404, 500).

---

### Q1: What is Express.js and Why Use It with Node.js?
**Question:** What is Express.js? What problems does it solve over raw Node.js `http` module?

**Answer:**
- **Express.js** is a fast, minimalist, unopinionated web application framework for Node.js.
- **Why use Express over raw `http` module?**:
  - Raw Node.js requires manual URL parsing, regex for routing, manual chunk concatenation for request bodies, and complex header management.
  - Express provides built-in routing, robust middleware pipeline, parameter extraction (`req.params`, `req.query`), JSON serialization (`res.json()`), and cookie/session handling.

---

### Q2: What is Middleware and What Does `next()` Do?
**Question:** What is middleware in Express? Explain the role of the `next()` function.

**Answer:**
- **Middleware**: A function that has access to the Request object (`req`), Response object (`res`), and the `next` function in the application's request-response cycle.
- **Role of `next()`**: Passes control to the **next middleware function in the stack**. If `next()` is not called (and `res.send()` is not returned), the request will hang indefinitely. If an argument is passed `next(err)`, Express immediately skips to the error-handling middleware.

---

### Q3: `app.use()` vs `app.get()`
**Question:** What is the difference between `app.use()` and `app.get()`?

**Answer:**
- **`app.use(path, middleware)`**: Matches **ALL HTTP methods** (GET, POST, PUT, DELETE) that start with the specified path prefix (or all routes if path omitted).
- **`app.get(path, handler)`**: Matches **ONLY HTTP GET requests** with an exact path match.

---

### Q4: HTTP Methods: PUT vs PATCH & DELETE vs GET
**Question:** Compare PUT vs PATCH and DELETE vs GET.

**Answer:**
- **`PUT`**: Replaces the **entire resource** with the new payload (Idempotent).
- **`PATCH`**: Applies **partial updates** to specific fields of a resource (Non-idempotent in theory, but typically idempotent).
- **`DELETE`**: Deletes a specific resource.
- **`GET`**: Retrieves data without modifying server state (Safe and Idempotent).

---

### Q5: HTTP Status Codes Overview
**Question:** Explain the most common HTTP status codes tested in interviews.

**Answer:**
- **2xx (Success)**:
  - `200 OK`: Standard successful request.
  - `201 Created`: Resource successfully created (POST/PUT).
  - `204 No Content`: Successful request with no body returned (DELETE).
- **4xx (Client Errors)**:
  - `400 Bad Request`: Malformed syntax or invalid request body.
  - `401 Unauthorized`: Authentication missing or invalid (Not logged in).
  - `403 Forbidden`: Authenticated, but user lacks permission (Logged in, but no access).
  - `404 Not Found`: Resource does not exist.
  - `429 Too Many Requests`: Rate limit exceeded.
- **5xx (Server Errors)**:
  - `500 Internal Server Error`: Unexpected server crash/exception.
  - `502 Bad Gateway`: Upstream server/proxy failure.
  - `503 Service Unavailable`: Server overloaded or down for maintenance.
