# 🚀 Full Stack Web & Mobile Engineering Master Interview Guide

<div align="center">

![Full Stack](https://img.shields.io/badge/Stack-MERN%20%7C%20React%20Native%20%7C%20SQL%20%7C%20System%20Design%20%7C%20Security%20%7C%20DSA-blue?style=for-the-badge)
![Difficulty](https://img.shields.io/badge/Levels-Easy%20%7C%20Medium%20%7C%20Hard%20%7C%20Coding%20Polyfills-green?style=for-the-badge)
![Total Modules](https://img.shields.io/badge/Modules-13%20Dedicated%20Sections-orange?style=for-the-badge)

**A complete, industry-standard technical preparation repository designed for Freshers, Junior, and Senior Full Stack & Frontend/Backend Developers.**

[Explore Domains](#-domain-navigation-matrix) • [Coding Challenges](#-machine-coding--polyfills) • [Scenario Architecture](#-full-stack-scenarios--system-design) • [Quick Revision Checklist](#-quick-interview-revision-checklist)

</div>

---

## 📚 Domain Navigation Matrix

| Domain | 🟢 Easy / Core | 🟡 Medium / Applied | 🔴 Hard / Advanced | 💻 Machine Coding / Queries |
| :--- | :--- | :--- | :--- | :--- |
| **📜 JavaScript** | [JS Easy](./JavaScript/JAVASCRIPT_EASY.md) | [JS Medium](./JavaScript/JAVASCRIPT_MEDIUM.md) | [JS Hard](./JavaScript/JAVASCRIPT_HARD.md) | [24-Topic Master Guide](./JavaScript/JAVASCRIPT_MASTER.md) • [Polyfills](./JavaScript/JAVASCRIPT_CODING.md) |
| **⚛️ React** | [React Easy](./React/REACT_EASY.md) | [React Medium](./React/REACT_MEDIUM.md) | [React Hard](./React/REACT_HARD.md) | [Hooks & Redux Flow](./React/REACT_MEDIUM.md) |
| **📱 React Native** | [RN Easy](./ReactNative/REACT_NATIVE_EASY.md) | [RN Medium](./ReactNative/REACT_NATIVE_MEDIUM.md) | [RN Hard](./ReactNative/REACT_NATIVE_HARD.md) | [Virtualization & JSI](./ReactNative/REACT_NATIVE_HARD.md) |
| **🟢 Node.js** | [Node Core Architecture](./Node.js/NODE_CORE.md) | [Event Loop & Streams](./Node.js/NODE_CORE.md) | [Cluster & Workers](./Node.js/NODE_CORE.md) | [Streams Compression](./Node.js/NODE_CORE.md) |
| **⚡ Express.js** | [Express Easy](./Node.js/Express/EXPRESS_EASY.md) | [Express Medium](./Node.js/Express/EXPRESS_MEDIUM.md) | [Express Hard](./Node.js/Express/EXPRESS_HARD.md) | [Middleware & Validation](./Node.js/Express/EXPRESS_MEDIUM.md) |
| **🍃 MongoDB** | [MongoDB Easy](./DATABASE/MongoDB/MONGODB_EASY.md) | [MongoDB Medium](./DATABASE/MongoDB/MONGODB_MEDIUM.md) | [MongoDB Hard](./DATABASE/MongoDB/MONGODB_HARD.md) | [Top 10 Mongo Queries](./DATABASE/MongoDB/MONGODB_CODING.md) |
| **🐬 MySQL & DBMS** | [DBMS Core](./DBMS/DBMS_CORE.md) | [MySQL Medium](./DATABASE/MySQL/MYSQL_MEDIUM.md) | [DBMS Hard](./DBMS/DBMS_HARD.md) | [Top 17 SQL Queries](./DATABASE/MySQL/SQL_CODING.md) |
| **🌐 Web & HTTP** | [HTTP / HTTPS / DNS](./WEB_HTTP/WEB_NETWORKING.md) | [WebSockets vs SSE](./WEB_HTTP/WEB_NETWORKING.md) | [CORS & Proxies](./WEB_HTTP/WEB_NETWORKING.md) | [google.com Lifecycle](./WEB_HTTP/WEB_NETWORKING.md) |
| **🔐 Auth & Security** | [Auth vs Authz](./SECURITY_AUTH/SECURITY_AUTHENTICATION.md) | [JWT & Bcrypt](./SECURITY_AUTH/SECURITY_AUTHENTICATION.md) | [XSS & CSRF Prevention](./SECURITY_AUTH/SECURITY_AUTHENTICATION.md) | [Refresh Token Rotation](./SECURITY_AUTH/SECURITY_AUTHENTICATION.md) |
| **🐙 Git & GitHub** | [Git vs GitHub](./GIT_GITHUB/GIT_GITHUB.md) | [Merge vs Rebase](./GIT_GITHUB/GIT_GITHUB.md) | [Reflog & Conflicts](./GIT_GITHUB/GIT_GITHUB.md) | [Undoing Commits](./GIT_GITHUB/GIT_GITHUB.md) |
| **🏗️ Scenarios** | [MERN Login Flow](./SCENARIO_BASED/FULLSTACK_SCENARIOS.md) | [1M Users Pagination](./SCENARIO_BASED/FULLSTACK_SCENARIOS.md) | [10k Concurrency & S3](./SCENARIO_BASED/FULLSTACK_SCENARIOS.md) | [Downtime Resilience](./SCENARIO_BASED/FULLSTACK_SCENARIOS.md) |
| **🎯 Project Guide** | [STAR Pitch Framework](./PROJECT_BASED/PROJECT_QUESTIONS.md) | [Debugging Hard Bugs](./PROJECT_BASED/PROJECT_QUESTIONS.md) | [Architecture Tradeoffs](./PROJECT_BASED/PROJECT_QUESTIONS.md) | [CI/CD & Scaling](./PROJECT_BASED/PROJECT_QUESTIONS.md) |
| **🌐 HTML & CSS** | [HTML Easy](./HTML/HTML_EASY.md) • [CSS Easy](./CSS/CSS_EASY.md) | [HTML Med](./HTML/HTML_MEDIUM.md) • [CSS Med](./CSS/CSS_MEDIUM.md) | [HTML Hard](./HTML/HTML_HARD.md) • [CSS Hard](./CSS/CSS_HARD.md) | [Flexbox / Grid Layouts](./CSS/CSS_MEDIUM.md) |
| **🧩 DSA & C++** | [DSA Easy](./DSA/DSA_EASY.md) • [C++ Easy](./CPP/CPP_EASY.md) | [DSA Med](./DSA/DSA_MEDIUM.md) • [C++ Med](./CPP/CPP_MEDIUM.md) | [DSA Hard](./DSA/DSA_HARD.md) • [C++ Hard](./CPP/CPP_HARD.md) | [Two Pointers / Trees / Kadane](./DSA/DSA_EASY.md) |

---

## 💻 Machine Coding & Polyfills

> [!TIP]
> Master implementation files located in [`JavaScript/JAVASCRIPT_CODING.md`](./JavaScript/JAVASCRIPT_CODING.md):

1. **`Array.prototype.myMap()`** (Handling sparse arrays & `thisArg`)
2. **`Array.prototype.myFilter()`**
3. **`Array.prototype.myReduce()`** (Handling initial values & empty array exceptions)
4. **Debounce Implementation** (Immediate leading-edge execution support)
5. **Throttle Implementation** (Leading and trailing call tracking)
6. **Deep Clone Implementation** (Handling circular references via `WeakMap`, Dates, Regex, Maps)
7. **Generic Memoization Function** (`memoize()`)
8. **Custom Promise Implementation** (`MyPromise` with Microtask chaining)
9. **Currying Function** (`curry()`)
10. **Flatten Array Recursive & Stack Iterative**

---

## 🏗️ Full-Stack Scenarios & System Design

- 🔐 **End-to-End MERN Login Flow**: [Read in FULLSTACK_SCENARIOS.md](./SCENARIO_BASED/FULLSTACK_SCENARIOS.md#q1-explain-the-complete-mern-login-flow-from-react-to-mongodb-and-back-)
- ⚡ **1 Million Records Keyset Cursor Pagination**: [Read in FULLSTACK_SCENARIOS.md](./SCENARIO_BASED/FULLSTACK_SCENARIOS.md#q2-how-would-you-implement-pagination-for-1-million-users-offset-vs-keyset)
- 🚀 **10,000 Concurrent Users Node.js Architecture**: [Read in FULLSTACK_SCENARIOS.md](./SCENARIO_BASED/FULLSTACK_SCENARIOS.md#q3-how-would-you-handle-10000-concurrent-users-on-a-nodejs-backend)
- 📦 **Direct S3 Presigned URL 500MB Uploads**: [Read in FULLSTACK_SCENARIOS.md](./SCENARIO_BASED/FULLSTACK_SCENARIOS.md#q4-how-would-you-upload-a-500mb-file-in-a-mern-application)

---

## ⚡ Quick Interview Revision Checklist

### 📜 JavaScript Core & Async
- [ ] Lexical Scope vs Dynamic Scope & Execution Context
- [ ] Scope Chain & Closures
- [ ] `var` vs `let` vs `const` & TDZ
- [ ] `call()`, `apply()`, `bind()` & Function Borrowing
- [ ] `this` keyword rules & Arrow Function Lexical `this`
- [ ] Shallow Copy vs Deep Copy (`structuredClone`)
- [ ] Event Loop: Call Stack $
ightarrow$ Microtasks (`Promises`, `nextTick`) $
ightarrow$ Macrotasks (`setTimeout`)
- [ ] Promise Combinators: `all`, `allSettled`, `race`, `any`
- [ ] Debouncing vs Throttling

### ⚛️ React & State
- [ ] Virtual DOM & Reconciliation Diffing
- [ ] React Fiber & Priority Lanes
- [ ] `useState` functional updates & React state batching
- [ ] `useEffect` dependency array & cleanup functions
- [ ] `useRef` vs `useState`
- [ ] `useMemo` vs `useCallback` (and when NOT to use `useMemo`)
- [ ] Context API vs Prop Drilling
- [ ] `useReducer` vs Redux Toolkit vs RTK Query

### 🟢 Node.js, Express & Security
- [ ] Libuv Event Loop 6 Phases
- [ ] Worker Threads vs Clustering vs Child Processes
- [ ] Streams, Buffers & Backpressure
- [ ] Express 5 Middleware Types & Centralized Error Handling
- [ ] JWT Access Token + Refresh Token Rotation
- [ ] Password Hashing with Bcrypt & Salting
- [ ] XSS vs CSRF Prevention (`HttpOnly`, `SameSite`)

### 🍃 Databases & System Design
- [ ] MongoDB 9 Index Types & `explain("executionStats")`
- [ ] Aggregation Pipeline (`$match`, `$group`, `$project`, `$lookup`, `$unwind`)
- [ ] ACID Properties & Isolation Levels
- [ ] Database Normalization 1NF, 2NF, 3NF, BCNF
- [ ] SQL Window Functions (`ROW_NUMBER`, `RANK`, `DENSE_RANK`)

---

<div align="center">

**⭐ Star this repository to keep it handy for quick revision before your interviews!**

*Created with ❤️ for aspiring Full Stack Developers.*

</div>
