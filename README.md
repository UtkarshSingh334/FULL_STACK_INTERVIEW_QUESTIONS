# 🚀 The Ultimate Full-Stack Developer Interview Mastery Guide
### *Comprehensive Questions, In-Depth Answers, Code Solutions & Architectural Deep-Dives*

> Curated and categorized by difficulty level (**🟢 Easy**, **🟡 Medium**, **🔴 Hard**) covering **HTML/CSS**, **JavaScript Engine & Modern ES6+**, **React & React Native**, **Node.js & Express Internals**, **Databases (SQL/NoSQL) & Redis**, and **Data Structures & Algorithms (DSA)**.

---

## 📑 Table of Contents

- [🟢 Level 1: EASY (Foundations & Core Fundamentals)](#-level-1-easy-foundations--core-fundamentals)
  - [HTML & CSS](#1-html--css)
    - [Q1.1: HTML vs HTML5 & Core Semantic Tags](#q11-html-vs-html5--core-semantic-tags)
    - [Q1.2: `href` vs `src` Attributes](#q12-href-vs-src-attributes)
    - [Q1.3: `<script>` Loading: Regular vs `async` vs `defer`](#q13-script-loading-regular-vs-async-vs-defer)
    - [Q1.4: Block vs Inline vs Inline-Block Elements](#q14-block-vs-inline-vs-inline-block-elements)
    - [Q1.5: CSS Position Types (`static`, `relative`, `absolute`, `fixed`, `sticky`)](#q15-css-position-types-static-relative-absolute-fixed-sticky)
    - [Q1.6: Flexbox vs CSS Grid](#q16-flexbox-vs-css-grid)
    - [Q1.7: Types of CSS (Inline, Internal, External, CSS Modules)](#q17-types-of-css-inline-internal-external-css-modules)
  - [JavaScript Basics](#2-javascript-basics)
    - [Q1.8: `var` vs `let` vs `const`, Hoisting & Temporal Dead Zone (TDZ)](#q18-var-vs-let-vs-const-hoisting--temporal-dead-zone-tdz)
    - [Q1.9: Data Types in JavaScript & Primitive vs Reference Types](#q19-data-types-in-javascript--primitive-vs-reference-types)
    - [Q1.10: Spread Operator (`...`) vs Rest Parameter (`...`)](#q110-spread-operator--vs-rest-parameter-)
    - [Q1.11: Object & Array Destructuring](#q111-object--array-destructuring)
    - [Q1.12: String Methods: `substring()` vs `substr()` vs `slice()`](#q112-string-methods-substring-vs-substr-vs-slice)
    - [Q1.13: DOM Manipulation: `getElementById`, `createElement`, `innerHTML`, `innerText`, `textContent`](#q113-dom-manipulation-getelementbyid-createelement-innerhtml-innertext-textcontent)
    - [Q1.14: `e.preventDefault()` vs `e.stopPropagation()`](#q114-epreventdefault-vs-estoppropagation)
    - [Q1.15: Pure Functions vs Impure Functions](#q115-pure-functions-vs-impure-functions)
    - [Q1.16: Arrow Functions vs Regular Functions](#q116-arrow-functions-vs-regular-functions)
  - [React Basics](#3-react-basics)
    - [Q1.17: State vs Props & State vs Hooks](#q117-state-vs-props--state-vs-hooks)
    - [Q1.18: Why does `console.log(state)` show the old value right after `setState`?](#q118-why-does-consolelogstate-show-the-old-value-right-after-setstate)
    - [Q1.19: `useEffect` Purpose & Dependency Array Variations (`[]`, `[dep]`, none)](#q119-useeffect-purpose--dependency-array-variations--dep-none)
    - [Q1.20: Lifting State Up in React](#q120-lifting-state-up-in-react)
  - [Node.js, Express & Databases Basics](#4-nodejs-express--databases-basics)
    - [Q1.21: Node.js Module Architecture (Core, Local, Third-Party)](#q121-nodejs-module-architecture-core-local-third-party)
    - [Q1.22: Why is `express.json()` used in Express apps?](#q122-why-is-expressjson-used-in-express-apps)
    - [Q1.23: GET vs POST in HTML Forms and REST APIs](#q123-get-vs-post-in-html-forms-and-rest-apis)
    - [Q1.24: SQL (Relational) vs NoSQL (Document/MongoDB)](#q124-sql-relational-vs-nosql-documentmongodb)
    - [Q1.25: What is Database Indexing & Single-Field Index?](#q125-what-is-database-indexing--single-field-index)
  - [DSA Easy](#5-dsa-easy)
    - [Q1.26: Swap Two Numbers Without a Third Variable](#q126-swap-two-numbers-without-a-third-variable)
    - [Q1.27: Check if a Number is Prime](#q127-check-if-a-number-is-prime)
    - [Q1.28: Check if a Number is an Armstrong Number](#q128-check-if-a-number-is-an-armstrong-number)
    - [Q1.29: Find the Largest Element in an Array](#q129-find-the-largest-element-in-an-array)
    - [Q1.30: Reverse a String (Multiple Approaches)](#q130-reverse-a-string-multiple-approaches)
    - [Q1.31: Factorial of a Number (Iterative & Recursive)](#q131-factorial-of-a-number-iterative--recursive)
    - [Q1.32: Find Missing Number in Array `[1..N]`](#q132-find-missing-number-in-array-1n)

---

- [🟡 Level 2: MEDIUM (Intermediate Mechanics, Practical Architecture & Algorithms)](#-level-2-medium-intermediate-mechanics-practical-architecture--algorithms)
  - [JavaScript Intermediate](#1-javascript-intermediate)
    - [Q2.1: Shallow Copy vs Deep Copy (Mechanics, Pitfalls & Solutions)](#q21-shallow-copy-vs-deep-copy-mechanics-pitfalls--solutions)
    - [Q2.2: `call()`, `apply()`, and `bind()` with Custom Polyfills](#q22-call-apply-and-bind-with-custom-polyfills)
    - [Q2.3: `map()` vs `filter()` vs `reduce()` with Complex Accumulations](#q23-map-vs-filter-vs-reduce-with-complex-accumulations)
    - [Q2.4: Scope Chaining, Lexical Scope & Closures](#q24-scope-chaining-lexical-scope--closures)
    - [Q2.5: Function Currying & Practical Real-World Implementations](#q25-function-currying--practical-real-world-implementations)
    - [Q2.6: Event Propagation: Bubbling, Capturing & Event Delegation](#q26-event-propagation-bubbling-capturing--event-delegation)
    - [Q2.7: Debouncing vs Throttling (with Production Implementations)](#q27-debouncing-vs-throttling-with-production-implementations)
    - [Q2.8: JavaScript Error Types: `ReferenceError`, `TypeError`, `SyntaxError`](#q28-javascript-error-types-referenceerror-typeerror-syntaxerror)
    - [Q2.9: JavaScript OOP & Prototypal Inheritance (`__proto__` vs `prototype`)](#q29-javascript-oop--prototypal-inheritance-__proto__-vs-prototype)
    - [Q2.10: Promises Deep Dive: States, `Promise.all`, `allSettled`, `race`, `any`, and Async/Await vs Callback Hell](#q210-promises-deep-dive-states-promiseall-allsettled-race-any-and-asyncawait-vs-callback-hell)
  - [React & React Native Intermediate](#2-react--react-native-intermediate)
    - [Q2.11: `useRef` Complete Guide: DOM Reference vs Mutable Instance Values](#q211-useref-complete-guide-dom-reference-vs-mutable-instance-values)
    - [Q2.12: React Performance Optimization: `React.memo`, `useMemo`, `useCallback`, Code Splitting](#q212-react-performance-optimization-reactmemo-usememo-usecallback-code-splitting)
    - [Q2.13: Cross-Origin Resource Sharing (CORS): Preflight, Headers & Express Config](#q213-cross-origin-resource-sharing-cors-preflight-headers--express-config)
    - [Q2.14: React Native: `ScrollView` vs `FlatList` vs `SafeAreaView` vs `map()`](#q214-react-native-scrollview-vs-flatlist-vs-safeareaview-vs-map)
    - [Q2.15: Horizontal Scrolling Implementation in React Native & CSS](#q215-horizontal-scrolling-implementation-in-react-native--css)
  - [Node.js, Express, Databases & Redis](#3-nodejs-express-databases--redis)
    - [Q2.16: Express Middleware Architecture & The BATER Types](#q216-express-middleware-architecture--the-bater-types)
    - [Q2.17: JWT (JSON Web Token) Complete Authentication & Token Refresh Flow](#q217-jwt-json-web-token-complete-authentication--token-refresh-flow)
    - [Q2.18: Why is `bcrypt` Used for Password Hashing Instead of SHA-256?](#q218-why-is-bcrypt-used-for-password-hashing-instead-of-sha-256)
    - [Q2.19: API Rate Limiting: Fixed Window vs Token Bucket Algorithms](#q219-api-rate-limiting-fixed-window-vs-token-bucket-algorithms)
    - [Q2.20: MongoDB `populate()` & Query Filtering Within Nested Populates](#q220-mongodb-populate--query-filtering-within-nested-populates)
    - [Q2.21: Compound Indexing in Databases & The ESR (Equality, Sort, Range) Rule](#q221-compound-indexing-in-databases--the-esr-equality-sort-range-rule)
    - [Q2.22: Redis Caching Architecture & Why It Is Not Always Used in Small Projects](#q222-redis-caching-architecture--why-it-is-not-always-used-in-small-projects)
  - [DSA Medium](#4-dsa-medium)
    - [Q2.23: Valid Parentheses (Stack)](#q223-valid-parentheses-stack)
    - [Q2.24: Happy Number (Floyd's Cycle-Finding Algorithm)](#q224-happy-number-floyds-cycle-finding-algorithm)
    - [Q2.25: Two Sum (Optimal Hash Map O(N))](#q225-two-sum-optimal-hash-map-on)
    - [Q2.26: Fibonacci Sequence (Iterative, Recursive, Dynamic Programming)](#q226-fibonacci-sequence-iterative-recursive-dynamic-programming)
    - [Q2.27: Rotate Array by K Positions (Reversal Algorithm O(1) Space)](#q227-rotate-array-by-k-positions-reversal-algorithm-o1-space)
    - [Q2.28: Sliding Window Technique: Maximum Sum Subarray of Size K](#q228-sliding-window-technique-maximum-sum-subarray-of-size-k)

---

- [🔴 Level 3: HARD (Advanced Engine Internals, Concurrency & Low-Level Architecture)](#-level-3-hard-advanced-engine-internals-concurrency--low-level-architecture)
  - [JavaScript & Engine Deep Internals](#1-javascript--engine-deep-internals)
    - [Q3.1: Complete Execution Breakdown of the `this` Keyword Across 6 Contexts](#q31-complete-execution-breakdown-of-the-this-keyword-across-6-contexts)
  - [Node.js Engine, Concurrency & React Native Architecture](#2-nodejs-engine-concurrency--react-native-architecture)
    - [Q3.2: Libuv Architecture: Event Loop Phases & Thread Pool (`UV_THREADPOOL_SIZE`)](#q32-libuv-architecture-event-loop-phases--thread-pool-uv_threadpool_size)
    - [Q3.3: Microtasks vs Macrotasks: `process.nextTick()` vs `setImmediate()` vs `setTimeout()`](#q33-microtasks-vs-macrotasks-processnexttick-vs-setimmediate-vs-settimeout)
    - [Q3.4: Node.js Buffer Internals & Raw Binary Memory Management](#q34-nodejs-buffer-internals--raw-binary-memory-management)
    - [Q3.5: Node.js Streams: Readable, Writable, Duplex, Transform, Piping & Backpressure](#q35-nodejs-streams-readable-writable-duplex-transform-piping--backpressure)
    - [Q3.6: File Systems, Streams & Threading: Node.js vs React Native Bridge/JSI Architecture](#q36-file-systems-streams--threading-nodejs-vs-react-native-bridgejsi-architecture)
    - [Q3.7: Multi-Process Concurrency: Node.js `cluster` Module & Worker Threads](#q37-multi-process-concurrency-nodejs-cluster-module--worker-threads)

---

# 🟢 Level 1: EASY (Foundations & Core Fundamentals)

---

## 1. HTML & CSS

### Q1.1: HTML vs HTML5 & Core Semantic Tags
**Question:** What are the key differences between HTML and HTML5? Why are semantic tags critical?

**Answer:**
- **HTML (HTML 4.01)**: Older standard relying heavily on generic `<div>` and `<span>` tags with classes for layout. Lacked native multimedia and storage support.
- **HTML5**: Modern web standard introducing native semantic layout tags (`<header>`, `<nav>`, `<main>`, `<article>`, `<section>`, `<aside>`, `<footer>`), native audio/video (`<audio>`, `<video>`), canvas graphics (`<canvas>`), client storage (`localStorage`, `sessionStorage`, `IndexedDB`), and enhanced form validation attributes (`required`, `pattern`, `type="email"`).

**Why Semantic Tags Matter:**
1. **Accessibility (a11y)**: Screen readers use semantic roles to navigate page structures.
2. **SEO**: Search engine crawlers understand content hierarchy (articles, main content, headers).
3. **Maintainability**: Clean, self-documenting code.

```html
<!-- HTML4 Legacy Approach -->
<div id="header">
  <div class="nav">...</div>
</div>
<div id="content">
  <div class="post">...</div>
</div>
<div id="footer">...</div>

<!-- HTML5 Semantic Approach -->
<header>
  <nav aria-label="Main Navigation">
    <ul><li><a href="#home">Home</a></li></ul>
  </nav>
</header>
<main>
  <article>
    <h1>Full Stack Guide</h1>
    <section>
      <h2>Semantic Structure</h2>
      <p>Semantic tags improve SEO and accessibility.</p>
    </section>
  </article>
  <aside>
    <h3>Related Links</h3>
  </aside>
</main>
<footer>
  <p>&copy; 2026 Developer Guide</p>
</footer>
```

---

### Q1.2: `href` vs `src` Attributes
**Question:** What is the fundamental difference between `href` (Hypertext Reference) and `src` (Source)?

**Answer:**
| Feature | `href` (Hypertext Reference) | `src` (Source) |
| :--- | :--- | :--- |
| **Meaning** | Points to an external resource to establish a link/relationship. | Points to a resource that is downloaded and embedded into the current document. |
| **Parsing Behavior** | **Non-blocking**: Browser fetches the resource asynchronously in the background without halting document parsing. | **Blocking (by default)**: Browser halts document parsing until the resource is downloaded, parsed, and executed. |
| **Common Elements** | `<a href="...">`, `<link rel="stylesheet" href="...">` | `<script src="...">`, `<img src="...">`, `<iframe src="...">` |

```html
<!-- href: Links the stylesheet without replacing the link tag -->
<link rel="stylesheet" href="styles.css" />

<!-- src: The image content replaces the img tag in DOM layout -->
<img src="avatar.png" alt="User Profile" />
```

---

### Q1.3: `<script>` Loading: Regular vs `async` vs `defer`
**Question:** Explain how `<script>`, `<script async>`, and `<script defer>` differ during HTML parsing and script execution.

**Answer:**
```
Regular:   HTML Parsing ===[PAUSE / Fetch & Exec Script]====> HTML Parsing Continues
Async:     HTML Parsing =======[Fetch Script in Parallel]====[PAUSE / Exec Script]==> HTML Parsing Continues
Defer:     HTML Parsing ======================================> [Exec Script after parsing completes]
```

- **Regular `<script>`**: HTML parsing pauses while the script is downloaded and immediately executed.
- **`<script async>`**: Script downloads in the background asynchronously. As soon as download completes, HTML parsing is **interrupted** to execute the script. Execution order is non-deterministic (whichever downloads first runs first). Ideal for independent scripts like Google Analytics.
- **`<script defer>`**: Script downloads in the background asynchronously. Execution is deferred until the entire HTML document is fully parsed (right before `DOMContentLoaded`). Scripts execute in the **exact order** they appear in the HTML. Ideal for scripts that depend on DOM or other scripts.

---

### Q1.4: Block vs Inline vs Inline-Block Elements
**Question:** Differentiate between `block`, `inline`, and `inline-block` display properties in CSS.

**Answer:**
| Property | Line Break | Width / Height Settable? | Margin / Padding Effects | Examples |
| :--- | :--- | :--- | :--- | :--- |
| `block` | Starts on a new line; occupies 100% parent width | ✅ Yes (`width: 300px; height: 100px`) | ✅ Full vertical & horizontal | `<div>`, `<p>`, `<h1>`-`<h6>`, `<section>` |
| `inline` | Sits on the same line as adjacent content | ❌ No (derived from content size) | ⚠️ Horizontal only (left/right). Vertical does not push siblings | `<span>`, `<a>`, `<strong>`, `<em>` |
| `inline-block` | Sits on the same line (flows inline) | ✅ Yes (`width`, `height` work) | ✅ Full vertical & horizontal | `<button>`, `<input>`, `<img>` |

---

### Q1.5: CSS Position Types (`static`, `relative`, `absolute`, `fixed`, `sticky`)
**Question:** Detail how the CSS `position` properties work and how they relate to the document flow.

**Answer:**
1. `static` (Default): Normal document flow. `top`, `left`, `right`, `bottom`, and `z-index` have no effect.
2. `relative`: Stays in the normal document flow, but offsets relative to its *own default position*. Its original space remains reserved in the DOM. Creates a positioning context for absolute children.
3. `absolute`: Removed from the normal document flow. Positioned relative to its nearest *non-static ancestor* (`relative`, `absolute`, `fixed`, or `sticky`). If none exists, positioned relative to `<html>`.
4. `fixed`: Removed from document flow. Positioned relative to the **viewport**. Does not scroll with the page (e.g., sticky navigation, modal backdrops).
5. `sticky`: Hybrid of `relative` and `fixed`. Acts as `relative` until the viewport scroll position crosses a specified threshold (e.g., `top: 0`), after which it sticks like `fixed` within its parent container.

```css
.card {
  position: relative; /* Context container */
  width: 300px;
  height: 200px;
}
.badge {
  position: absolute;
  top: 10px;
  right: 10px; /* Positioned at top-right of .card */
}
.sticky-header {
  position: sticky;
  top: 0;
  z-index: 100; /* Stays fixed at top when scrolling past */
}
```

---

### Q1.6: Flexbox vs CSS Grid
**Question:** When should you use Flexbox vs CSS Grid?

**Answer:**
- **Flexbox (1-Dimensional)**: Designed for laying items out along a **single axis** (either row OR column). Ideal for navigation bars, centering items, distributing space inside cards, or dynamic resizing based on content.
- **CSS Grid (2-Dimensional)**: Designed for laying items out across **both rows AND columns simultaneously**. Ideal for entire page layouts, photo galleries, dashboards, and complex overlapping grid systems.

```css
/* Flexbox Example: Centering and Distribution */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/* Grid Example: Responsive 2D Dashboard */
.dashboard {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}
```

---

### Q1.7: Types of CSS (Inline, Internal, External, CSS Modules)
**Question:** Explain the different ways to style web applications and their specificity/maintainability trade-offs.

**Answer:**
1. **Inline CSS**: Defined in HTML `style="..."` attribute. Specificity: Highest (`1-0-0-0`). Violates separation of concerns; avoid in production except for dynamic JavaScript styles.
2. **Internal CSS**: Defined inside `<style>` tags in the `<head>`. Useful for single-page standalone documents.
3. **External CSS**: Linked via `<link rel="stylesheet" href="...">`. Browser caches the file across pages; standard for classic web apps.
4. **CSS Modules / Scoped CSS**: Class names are hashed uniquely at build time (e.g., `.button_a8f9z`), completely eliminating global namespace pollution in React/Next.js/Vue.

---

## 2. JavaScript Basics

### Q1.8: `var` vs `let` vs `const`, Hoisting & Temporal Dead Zone (TDZ)
**Question:** Explain the exact differences between `var`, `let`, and `const`, including hoisting behavior and the Temporal Dead Zone (TDZ).

**Answer:**
| Feature | `var` | `let` | `const` |
| :--- | :--- | :--- | :--- |
| **Scope** | Function Scope | Block Scope (`{}`) | Block Scope (`{}`) |
| **Hoisting** | Hoisted & initialized to `undefined` | Hoisted but placed in **TDZ** | Hoisted but placed in **TDZ** |
| **Re-declaration** | Allowed in same scope | Throws `SyntaxError` | Throws `SyntaxError` |
| **Re-assignment** | Allowed | Allowed | Throws `TypeError` |

**What is the Temporal Dead Zone (TDZ)?**
The TDZ is the time window between entering a block scope and the variable declaration being evaluated. Accessing a `let` or `const` variable in its TDZ throws a `ReferenceError`.

```javascript
console.log(a); // undefined (var hoisted & initialized)
// console.log(b); // ReferenceError: Cannot access 'b' before initialization (TDZ)

var a = 10;
let b = 20; // TDZ for 'b' ends here

{
  // Block scope demonstration
  var x = 100;
  let y = 200;
}
console.log(x); // 100 (leaked out of block)
// console.log(y); // ReferenceError: y is not defined
```

---

### Q1.9: Data Types in JavaScript & Primitive vs Reference Types
**Question:** List all JavaScript data types and explain how Primitive and Reference types are stored in memory.

**Answer:**
- **7 Primitive Data Types** (Stored directly in the **Stack**, immutable by value):
  1. `string`
  2. `number` (includes `NaN`, `Infinity`)
  3. `bigint` (`123n`)
  4. `boolean`
  5. `undefined`
  6. `symbol` (`Symbol('id')`)
  7. `null` (Note: `typeof null === 'object'` is a legacy JS quirk)
- **Reference Types** (Stored in the **Heap**, variables hold stack pointers to heap addresses):
  - `Object`, `Array`, `Function`, `Date`, `RegExp`, `Map`, `Set`.

```javascript
// Primitive: Pass-by-value
let a = 10;
let b = a;
b = 20;
console.log(a); // 10 (unchanged)

// Reference: Pass-by-reference
let obj1 = { name: "Alice" };
let obj2 = obj1;
obj2.name = "Bob";
console.log(obj1.name); // "Bob" (mutated heap data)
```

---

### Q1.10: Spread Operator (`...`) vs Rest Parameter (`...`)
**Question:** How does the three-dot syntax (`...`) behave as a Spread operator vs Rest parameter?

**Answer:**
- **Spread Operator**: Unpacks / expands elements of an array or properties of an object into individual elements.
- **Rest Parameter**: Collects / condenses multiple individual arguments into a single array structure.

```javascript
// Rest: Collects remaining arguments into an array
function sumNumbers(multiplier, ...numbers) {
  return numbers.map((n) => n * multiplier);
}
console.log(sumNumbers(2, 10, 20, 30)); // [20, 40, 60]

// Spread: Expands array elements or object properties
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5]; // [1, 2, 3, 4, 5]

const user = { name: "Utkarsh", role: "Dev" };
const updatedUser = { ...user, city: "Bangalore" };
```

---

### Q1.11: Object & Array Destructuring
**Question:** Show how to extract values cleanly using object and array destructuring, with aliases and default values.

```javascript
// Array Destructuring
const coordinates = [12.9716, 77.5946];
const [lat, lng, elevation = 920] = coordinates;

// Swapping variables with destructuring
let x = 5, y = 10;
[x, y] = [y, x];
console.log(x, y); // 10, 5

// Object Destructuring with Rename & Defaults
const response = {
  data: { userId: 101, username: "utkarsh_s" },
  status: 200
};

const {
  data: { userId: id, username },
  status: httpStatus = 500
} = response;

console.log(id, username, httpStatus); // 101, "utkarsh_s", 200
```

---

### Q1.12: String Methods: `substring()` vs `substr()` vs `slice()`
**Question:** Compare `substring()`, `substr()`, and `slice()` with edge cases like negative indices.

**Answer:**
| Method | Syntax | Handles Negative Index? | Swaps `start > end`? | Deprecation Status |
| :--- | :--- | :--- | :--- | :--- |
| `slice(start, end)` | `(start, end)` (end non-inclusive) | ✅ Counts backwards from string length | ❌ Returns `""` if `start > end` | Standard & Recommended |
| `substring(start, end)` | `(start, end)` (end non-inclusive) | ❌ Treats negative as `0` | ✅ Swaps arguments if `start > end` | Standard |
| `substr(start, length)` | `(start, length)` | ✅ Negative `start` counts from end | N/A (second arg is length) | ⚠️ **Deprecated** (Legacy) |

```javascript
const str = "JavaScript";

console.log(str.slice(0, 4));      // "Java"
console.log(str.slice(-6));        // "Script" (counts 6 from end)
console.log(str.slice(4, 0));      // ""

console.log(str.substring(4, 0));  // "Java" (swaps arguments to 0, 4)
console.log(str.substring(-4));    // "JavaScript" (negative becomes 0)
```

---

### Q1.13: DOM Manipulation: `getElementById`, `createElement`, `innerHTML`, `innerText`, `textContent`
**Question:** Differentiate between `innerHTML`, `innerText`, and `textContent`.

**Answer:**
- `innerHTML`: Returns or parses raw HTML tags. ⚠️ **Security Risk**: Subject to Cross-Site Scripting (XSS) if unsanitized user input is inserted.
- `innerText`: Returns only visible text rendered on screen. **Trigger Layout Reflow**: Aware of CSS styling (respects `display: none` or `visibility: hidden` and excludes them). Slower because it computes layout.
- `textContent`: Returns raw text content of all nodes inside the element, including `<script>`, `<style>`, and hidden elements (`display: none`). Does **not** trigger reflow, making it faster and safer.

```javascript
const container = document.getElementById("root");

// Create element safely
const newDiv = document.createElement("div");
newDiv.textContent = "Safe Text Content"; // No XSS risk
container.appendChild(newDiv);
```

---

### Q1.14: `e.preventDefault()` vs `e.stopPropagation()`
**Question:** What does `e.preventDefault()` do compared to `e.stopPropagation()`?

**Answer:**
- `e.preventDefault()`: Prevents the **default browser behavior** associated with an event (e.g., stops `<form>` submission from refreshing the page, or stops `<a href="...">` from navigating). It does **not** stop the event from bubbling up the DOM.
- `e.stopPropagation()`: Stops the event from traveling up (bubbling) or down (capturing) the DOM tree. It does **not** prevent browser default actions.

---

### Q1.15: Pure Functions vs Impure Functions
**Question:** Define a pure function and why it is essential in modern state management (React / Redux).

**Answer:**
A **Pure Function** satisfies two rules:
1. **Deterministic**: Given the exact same arguments, it always returns the exact same output.
2. **No Side Effects**: It does not mutate external state, modify input arguments, or perform I/O operations (like API calls, console.log, DOM manipulation, or `Date.now()`).

```javascript
// Pure Function
const add = (a, b) => a + b;

// Impure Function (mutates external variable + relies on external state)
let counter = 0;
const increment = (value) => {
  counter += value; // Side effect
  return counter;
};
```

---

### Q1.16: Arrow Functions vs Regular Functions
**Question:** Explain how arrow functions differ from regular ES5 functions.

**Answer:**
1. **`this` Binding**: Regular functions have their own dynamic `this` determined by *how they are called*. Arrow functions do **not** have their own `this`; they capture `this` lexically from their enclosing lexical context.
2. **`arguments` Object**: Regular functions have an `arguments` object. Arrow functions do not (use Rest `...args` instead).
3. **Constructor Capability**: Regular functions can be invoked with `new Person()`. Arrow functions cannot be used as constructors and will throw `TypeError`.
4. **No `prototype`**: Arrow functions do not have a `.prototype` property.

---

## 3. React Basics

### Q1.17: State vs Props & State vs Hooks
**Question:** Compare State vs Props and explain the concept of Hooks in React.

**Answer:**
- **Props (Properties)**: Read-only data passed from parent component to child component. Component cannot mutate its own props (unidirectional data flow).
- **State**: Mutable, local data managed internally within a component. Changing state triggers a re-render of the component and its children.
- **Hooks**: Functions introduced in React 16.8 that allow functional components to hook into React state and lifecycle features without writing ES6 class components (e.g., `useState`, `useEffect`, `useContext`).

---

### Q1.18: Why does `console.log(state)` show the old value right after `setState`?
**Question:** Explain why state changes in React are not reflected immediately in subsequent lines of code.

**Answer:**
State updates in React are **asynchronous and batched** for performance optimization. When you call `setCount(count + 1)`, React schedules a state transition and marks the component for a re-render. The current execution context still retains the value from the closure of the current render pass.

```jsx
const [count, setCount] = useState(0);

const handleClick = () => {
  setCount(count + 1);
  console.log(count); // Prints 0, NOT 1!
};

// Solution 1: Use useEffect to listen to state updates
useEffect(() => {
  console.log("Updated Count:", count); // Runs after state commit & render
}, [count]);

// Solution 2: For consecutive updates, use updater function pattern
setCount((prev) => prev + 1);
setCount((prev) => prev + 1); // Correctly increments by 2
```

---

### Q1.19: `useEffect` Purpose & Dependency Array Variations (`[]`, `[dep]`, none)
**Question:** Explain the lifecycle mapping of `useEffect` based on its dependency array.

**Answer:**
```jsx
// 1. No dependency array: Runs after EVERY single render
useEffect(() => {
  console.log("Runs on mount and EVERY re-render");
});

// 2. Empty array []: Runs ONCE after initial mount (ComponentDidMount)
useEffect(() => {
  console.log("Runs only ONCE after mount");
  
  // Cleanup function runs on unmount (ComponentWillUnmount)
  return () => {
    console.log("Cleanup on unmount (e.g., remove event listeners, timers)");
  };
}, []);

// 3. With dependencies [count]: Runs on mount + whenever 'count' changes
useEffect(() => {
  console.log("Runs on mount and whenever 'count' changes");
  
  return () => {
    console.log("Cleanup runs BEFORE next effect execution or unmount");
  };
}, [count]);
```

---

### Q1.20: Lifting State Up in React
**Question:** What does "Lifting State Up" mean, and when should you use it?

**Answer:**
When two or more sibling components need access to the same state or need to synchronize changes, you lift the shared state up to their **closest common parent ancestor**. The parent manages the state and passes down the state value via props and updater callback functions to the children.

```jsx
// Parent Component
function TemperatureApp() {
  const [celsius, setCelsius] = useState(0);
  return (
    <div>
      <CelsiusInput value={celsius} onChange={setCelsius} />
      <FahrenheitDisplay celsius={celsius} />
    </div>
  );
}
```

---

## 4. Node.js, Express & Databases Basics

### Q1.21: Node.js Module Architecture (Core, Local, Third-Party)
**Question:** How does Node.js handle modularity? Differentiate between module types and CommonJS vs ESM.

**Answer:**
1. **Core Modules**: Built into Node.js binary (e.g., `fs`, `path`, `http`, `crypto`, `os`). Loaded without path prefix: `require('fs')`.
2. **Local Modules**: Files created in your application: `require('./utils/math')`.
3. **Third-Party Modules**: Installed via npm into `node_modules`: `require('express')`.

- **CommonJS (CJS)**: Synchronous loading using `require()` and `module.exports`.
- **ECMAScript Modules (ESM)**: Asynchronous standard using `import / export` (`"type": "module"` in `package.json`).

---

### Q1.22: Why is `express.json()` used in Express apps?
**Question:** Why does `req.body` return `undefined` without `express.json()`?

**Answer:**
By default, Node.js streams HTTP incoming request payloads in raw binary chunks (`Buffers`). Express does not automatically parse incoming JSON payloads into JavaScript objects. `express.json()` is a built-in middleware that listens to incoming `data` chunks, concatenates them, parses the JSON string, and populates `req.body`.

```javascript
const express = require('express');
const app = express();

// Required to parse application/json payloads
app.use(express.json());

app.post('/api/users', (req, res) => {
  console.log(req.body); // Defined JS Object { name: 'Utkarsh' }
  res.status(201).json({ success: true, user: req.body });
});
```

---

### Q1.23: GET vs POST in HTML Forms and REST APIs
**Question:** Contrast GET and POST methods in terms of data transmission, caching, and idempotency.

**Answer:**
| Feature | GET | POST |
| :--- | :--- | :--- |
| **Data Location** | URL Query Parameters (`/search?q=nodejs`) | Request Body (`payload`) |
| **Idempotency** | ✅ Idempotent (multiple requests yield same result) | ❌ Non-Idempotent (repeated requests create new records) |
| **Caching & History** | Cached by browsers and stored in browser history | Not cached by default; not stored in history |
| **Data Size Limit** | Limited by URL length limit (~2048 chars) | No fixed limit (configured on server) |
| **Security** | Insecure for sensitive data (visible in URL logs) | Secure for sensitive data (payload encrypted over HTTPS) |

---

### Q1.24: SQL (Relational) vs NoSQL (Document/MongoDB)
**Question:** When should you choose SQL vs NoSQL?

**Answer:**
- **SQL (PostgreSQL, MySQL)**: Relational, rigid tabular schema, normalized tables with foreign key relationships, ACID transactions guaranteed. Best for financial systems, complex join queries, and structured schemas.
- **NoSQL (MongoDB, DynamoDB)**: Document-oriented, flexible schema (JSON/BSON), hierarchical nested objects, horizontal scaling (sharding). Best for real-time big data, rapidly evolving schemas, IoT, and content management.

---

### Q1.25: What is Database Indexing & Single-Field Index?
**Question:** How does a database index work and what is a single-field index?

**Answer:**
Without an index, a database must perform a **Full Collection/Table Scan** ($O(N)$), reading every single row from disk. An index creates a specialized data structure (typically a **B-Tree**) storing field values sorted alongside pointers to actual disk records, reducing search complexity to $O(\log N)$.

```javascript
// MongoDB Single-Field Index
// Creates ascending index on email field
db.users.createIndex({ email: 1 });
```

---

## 5. DSA Easy

### Q1.26: Swap Two Numbers Without a Third Variable
**Problem:** Swap `a` and `b` in $O(1)$ auxiliary memory.

```javascript
// Approach 1: Bitwise XOR (Best - No integer overflow risk)
function swapXOR(a, b) {
  a = a ^ b;
  b = a ^ b;
  a = a ^ b;
  return [a, b];
}

// Approach 2: Arithmetic (Addition & Subtraction)
function swapArithmetic(a, b) {
  a = a + b;
  b = a - b;
  a = a - b;
  return [a, b];
}

// Approach 3: ES6 Destructuring
function swapDestructuring(a, b) {
  [a, b] = [b, a];
  return [a, b];
}
```

---

### Q1.27: Check if a Number is Prime
**Problem:** Determine if integer $N > 1$ is prime in $O(\sqrt{N})$ time.

```javascript
function isPrime(n) {
  if (n <= 1) return false;
  if (n <= 3) return true;
  if (n % 2 === 0 || n % 3 === 0) return false;

  // Check divisors of form 6k ± 1 up to sqrt(n)
  for (let i = 5; i * i <= n; i += 6) {
    if (n % i === 0 || n % (i + 2) === 0) return false;
  }
  return true;
}

console.log(isPrime(29)); // true
console.log(isPrime(49)); // false
```

---

### Q1.28: Check if a Number is an Armstrong Number
**Problem:** An Armstrong (narcissistic) number equals the sum of its digits each raised to the power of the number of digits (e.g., $153 = 1^3 + 5^3 + 3^3$).

```javascript
function isArmstrong(num) {
  const digits = String(num).split('').map(Number);
  const power = digits.length;
  const sum = digits.reduce((acc, digit) => acc + Math.pow(digit, power), 0);
  return sum === num;
}

console.log(isArmstrong(153));  // true (1 + 125 + 27 = 153)
console.log(isArmstrong(9474)); // true (9^4 + 4^4 + 7^4 + 4^4 = 9474)
console.log(isArmstrong(123));  // false
```

---

### Q1.29: Find the Largest Element in an Array
**Problem:** Find the maximum value in an array in $O(N)$ time.

```javascript
function findLargest(arr) {
  if (!arr || arr.length === 0) return null;
  let max = arr[0];
  for (let i = 1; i < arr.length; i++) {
    if (arr[i] > max) {
      max = arr[i];
    }
  }
  return max;
}

console.log(findLargest([12, 45, 67, 2, 99, 34])); // 99
```

---

### Q1.30: Reverse a String (Multiple Approaches)
**Problem:** Reverse a given string.

```javascript
// Approach 1: Built-in methods
const reverseStr1 = (str) => str.split('').reverse().join('');

// Approach 2: In-place two pointers using character array (O(N) time, O(1) extra space)
function reverseStr2(str) {
  const chars = str.split('');
  let left = 0, right = chars.length - 1;
  while (left < right) {
    [chars[left], chars[right]] = [chars[right], chars[left]];
    left++;
    right--;
  }
  return chars.join('');
}

// Approach 3: Recursion
function reverseStrRecursive(str) {
  if (str === "") return "";
  return reverseStrRecursive(str.substr(1)) + str.charAt(0);
}
```

---

### Q1.31: Factorial of a Number (Iterative & Recursive)
**Problem:** Calculate $N! = N \times (N-1) \times \dots \times 1$.

```javascript
// Iterative: O(N) Time, O(1) Space
function factorialIterative(n) {
  if (n < 0) return -1;
  let result = 1;
  for (let i = 2; i <= n; i++) {
    result *= i;
  }
  return result;
}

// Recursive: O(N) Time, O(N) Call Stack
function factorialRecursive(n) {
  if (n < 0) return -1;
  if (n === 0 || n === 1) return 1;
  return n * factorialRecursive(n - 1);
}
```

---

### Q1.32: Find Missing Number in Array `[1..N]`
**Problem:** Given an array containing $N-1$ distinct integers in the range $[1, N]$, find the missing number in $O(N)$ time and $O(1)$ space.

```javascript
// Approach 1: Sum Formula (Sum of 1..N is N*(N+1)/2)
function findMissingSum(arr, n) {
  const expectedSum = (n * (n + 1)) / 2;
  const actualSum = arr.reduce((acc, curr) => acc + curr, 0);
  return expectedSum - actualSum;
}

// Approach 2: Bitwise XOR (Prevents integer overflow for huge numbers)
function findMissingXOR(arr, n) {
  let xor1 = 0;
  let xor2 = 0;
  for (let i = 1; i <= n; i++) xor1 ^= i;
  for (let num of arr) xor2 ^= num;
  return xor1 ^ xor2;
}

console.log(findMissingXOR([1, 2, 4, 5, 6], 6)); // 3
```

---

# 🟡 Level 2: MEDIUM (Intermediate Mechanics, Practical Architecture & Algorithms)

---

## 1. JavaScript Intermediate

### Q2.1: Shallow Copy vs Deep Copy (Mechanics, Pitfalls & Solutions)
**Question:** Explain the difference between Shallow Copy and Deep Copy in JavaScript. What are the limitations of `JSON.parse(JSON.stringify(obj))`?

**Answer:**
- **Shallow Copy**: Copies the top-level properties. If a property value is a reference to an object/array, only the **memory address reference** is copied. Changes to nested objects affect both copies.
- **Deep Copy**: Recursively duplicates all nested objects and arrays into brand new heap memory allocations. Changes to nested structures are completely isolated.

**Methods Comparison:**
```javascript
const original = {
  name: "Utkarsh",
  skills: ["React", "Node"],
  date: new Date(),
  calc: function() { return 42; },
  sym: Symbol("id"),
  undef: undefined
};

// 1. Shallow Copy (Spread / Object.assign)
const shallow = { ...original };
shallow.skills.push("MongoDB");
console.log(original.skills); // ['React', 'Node', 'MongoDB'] -> Mutated!

// 2. JSON.parse(JSON.stringify(obj)) Pitfalls:
// - Loses functions, undefined, and Symbol properties
// - Converts Date objects into ISO string representations
// - Throws TypeError on circular references
const jsonCopy = JSON.parse(JSON.stringify(original));
console.log(typeof jsonCopy.date); // 'string' (Lost Date instance!)
console.log(jsonCopy.calc);        // undefined (Lost function!)

// 3. Modern Standard: structuredClone() (Supported in Node 17+ and all modern browsers)
const deepCopy = structuredClone(original);
// Retains Date, Set, Map, ArrayBuffer, RegExp & handles circular references
```

**Custom Recursive Deep Clone Polyfill:**
```javascript
function deepClone(obj, hash = new WeakMap()) {
  if (Object(obj) !== obj) return obj; // Primitives
  if (obj instanceof Date) return new Date(obj);
  if (obj instanceof RegExp) return new RegExp(obj.source, obj.flags);
  if (hash.has(obj)) return hash.get(obj); // Handle Circular References

  const result = Array.isArray(obj) ? [] : Object.create(Object.getPrototypeOf(obj));
  hash.set(obj, result);

  for (const key of Reflect.ownKeys(obj)) {
    result[key] = deepClone(obj[key], hash);
  }
  return result;
}
```

---

### Q2.2: `call()`, `apply()`, and `bind()` with Custom Polyfills
**Question:** Compare `call`, `apply`, and `bind`. Write production-ready polyfills for `bind` and `apply`.

**Answer:**
- `call(thisArg, arg1, arg2, ...)`: Invokes function immediately with given `this` and comma-separated arguments.
- `apply(thisArg, [argsArray])`: Invokes function immediately with given `this` and arguments passed as an array.
- `bind(thisArg, arg1, arg2, ...)`: Returns a **new function** permanently bound to `thisArg` and preset arguments, to be invoked later.

```javascript
const person = {
  fullName: function(city, country) {
    return `${this.firstName} ${this.lastName} from ${city}, ${country}`;
  }
};
const user = { firstName: "Utkarsh", lastName: "Singh" };

console.log(person.fullName.call(user, "Bangalore", "India"));
console.log(person.fullName.apply(user, ["Bangalore", "India"]));

const boundFunc = person.fullName.bind(user, "Bangalore");
console.log(boundFunc("India"));
```

**Custom Polyfill for `myBind`:**
```javascript
Function.prototype.myBind = function(context, ...boundArgs) {
  if (typeof this !== 'function') {
    throw new TypeError('myBind must be called on a function');
  }
  const fn = this;
  return function(...callArgs) {
    return fn.apply(context, [...boundArgs, ...callArgs]);
  };
};
```

---

### Q2.3: `map()` vs `filter()` vs `reduce()` with Complex Accumulations
**Question:** Compare `map`, `filter`, and `reduce`. Show how to implement grouping and flatMap using `reduce`.

```javascript
const transactions = [
  { id: 1, type: "income", amount: 1000, category: "salary" },
  { id: 2, type: "expense", amount: 200, category: "food" },
  { id: 3, type: "expense", amount: 300, category: "rent" },
  { id: 4, type: "income", amount: 500, category: "freelance" }
];

// Complex Accumulation with reduce(): Grouping & Totals in Single Pass O(N)
const report = transactions.reduce((acc, curr) => {
  acc.totalBalance += curr.type === "income" ? curr.amount : -curr.amount;
  acc.byType[curr.type] = (acc.byType[curr.type] || 0) + curr.amount;
  acc.categories.push(curr.category);
  return acc;
}, { totalBalance: 0, byType: {}, categories: [] });

console.log(report);
/*
{
  totalBalance: 1000,
  byType: { income: 1500, expense: 500 },
  categories: [ 'salary', 'food', 'rent', 'freelance' ]
}
*/
```

---

### Q2.4: Scope Chaining, Lexical Scope & Closures
**Question:** How does the JavaScript engine resolve identifiers across nested scopes? What creates a closure?

**Answer:**
- **Lexical Scope**: Scope is determined by where variables and blocks are authored in the code at write-time, not at runtime.
- **Scope Chain**: When a variable is referenced, the JS engine searches the immediate Local Scope. If not found, it traverses upward to outer enclosing scopes until reaching the Global Scope. If still unresolved, it throws a `ReferenceError`.
- **Closure**: A function bundled together with references to its lexical environment. A closure allows an inner function to remember and access variables from its outer enclosing function even after that outer function has returned and exited the call stack.

```javascript
function createCounter(initialValue = 0) {
  let count = initialValue; // Private encapsulated variable
  return {
    increment: () => ++count,
    decrement: () => --count,
    getValue: () => count
  };
}

const counter = createCounter(5);
console.log(counter.increment()); // 6
console.log(counter.getValue());   // 6
// 'count' cannot be directly accessed or modified externally!
```

---

### Q2.5: Function Currying & Practical Real-World Implementations
**Question:** What is Currying? Write an infinite curry function `sum(1)(2)(3)...()`.

**Answer:**
**Currying** is a functional programming technique where a function with multiple arguments $f(a, b, c)$ is transformed into a sequence of unary functions $f(a)(b)(c)$.

```javascript
// Infinite Currying Function
function sum(a) {
  return function(b) {
    if (b !== undefined) {
      return sum(a + b);
    }
    return a;
  };
}

console.log(sum(1)(2)(3)(4)()); // 10

// Practical Real-World Use Case: Logging utility
const logger = (date) => (severity) => (message) =>
  `[${date.toISOString()}] [${severity.toUpperCase()}]: ${message}`;

const logNow = logger(new Date());
const logErrorNow = logNow("ERROR");

console.log(logErrorNow("Database connection timeout"));
```

---

### Q2.6: Event Propagation: Bubbling, Capturing & Event Delegation
**Question:** Explain the 3 phases of event propagation and how Event Delegation optimizes DOM memory.

**Answer:**
1. **Capturing Phase**: Event trickles down from `window` -> `document` -> `<html>` -> `<body>` -> Target Element.
2. **Target Phase**: Event reaches the target element that initiated the action.
3. **Bubbling Phase** (Default): Event bubbles up from Target Element -> `<body>` -> `<html>` -> `document` -> `window`.

**Event Delegation**:
Instead of attaching 10,000 event listeners to individual list items (`<li>`), attach **one listener** to the parent container (`<ul>`) and leverage event bubbling with `e.target`.

```javascript
const userList = document.getElementById("user-list");

userList.addEventListener("click", (e) => {
  // Check if a delete button inside any list item was clicked
  if (e.target && e.target.matches("button.delete-btn")) {
    const userId = e.target.dataset.userId;
    console.log(`Deleting User ID: ${userId}`);
    e.target.closest("li").remove();
  }
});
```

---

### Q2.7: Debouncing vs Throttling (with Production Implementations)
**Question:** Differentiate Debouncing vs Throttling and implement both.

**Answer:**
- **Debouncing**: Delays execution of a function until a specified idle duration has passed since the *last* invocation. If invoked again before the timer expires, the timer resets. Ideal for search autocompletes, window resize, auto-saving drafts.
- **Throttling**: Ensures a function is executed at most once in a given time interval, ignoring all intermediate calls. Ideal for scroll position listeners, gaming actions (button spamming), mouse moves.

```javascript
// Debounce Implementation
function debounce(fn, delay) {
  let timerId;
  return function(...args) {
    clearTimeout(timerId);
    timerId = setTimeout(() => {
      fn.apply(this, args);
    }, delay);
  };
}

// Throttle Implementation
function throttle(fn, limit) {
  let inThrottle = false;
  return function(...args) {
    if (!inThrottle) {
      fn.apply(this, args);
      inThrottle = true;
      setTimeout(() => {
        inThrottle = false;
      }, limit);
    }
  };
}
```

---

### Q2.8: JavaScript Error Types: `ReferenceError`, `TypeError`, `SyntaxError`
**Question:** Explain common JavaScript error types and when each is thrown.

**Answer:**
1. **`ReferenceError`**: Thrown when attempting to access a variable that has not been declared, or accessing a `let`/`const` variable in its Temporal Dead Zone (TDZ).
   ```javascript
   console.log(unknownVar); // ReferenceError: unknownVar is not defined
   ```
2. **`TypeError`**: Thrown when an operation is performed on a value of the incorrect data type (e.g., calling non-function, accessing property on `null`/`undefined`, reassigning `const`).
   ```javascript
   const x = 10;
   x = 20; // TypeError: Assignment to constant variable
   null.foo(); // TypeError: Cannot read properties of null
   ```
3. **`SyntaxError`**: Thrown at compile/parse time when JavaScript code violates language grammar rules.
   ```javascript
   // let const = 10; // SyntaxError: Unexpected token 'const'
   ```

---

### Q2.9: JavaScript OOP & Prototypal Inheritance (`__proto__` vs `prototype`)
**Question:** How does prototypal inheritance work in JavaScript? Differentiate `prototype` vs `__proto__`.

**Answer:**
- `prototype`: A property present on **constructor functions / classes** that specifies properties/methods to be inherited by all instances created with `new`.
- `__proto__`: An internal accessor property on every object **instance** pointing to the prototype object of its constructor (`instance.__proto__ === Constructor.prototype`).

```javascript
function Animal(name) {
  this.name = name;
}
Animal.prototype.speak = function() {
  return `${this.name} makes a noise.`;
};

function Dog(name, breed) {
  Animal.call(this, name); // Super constructor call
  this.breed = breed;
}

// Set up prototypal inheritance chain
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;

Dog.prototype.bark = function() {
  return `${this.name} barks loudly!`;
};

const d = new Dog("Buddy", "Golden Retriever");
console.log(d.bark());  // "Buddy barks loudly!"
console.log(d.speak()); // "Buddy makes a noise." (Traversed prototype chain)
```

---

### Q2.10: Promises Deep Dive: States, `Promise.all`, `allSettled`, `race`, `any`, and Async/Await vs Callback Hell
**Question:** Compare all Promise combinator methods and explain how `async/await` eliminates callback hell.

**Answer:**
```javascript
// Promise Combinators:
// 1. Promise.all([p1, p2]): Fails FAST if ANY promise rejects. Resolves when ALL resolve.
Promise.all([fetchUsers(), fetchPosts()])
  .then(([users, posts]) => console.log(users, posts))
  .catch(err => console.error("One failed:", err));

// 2. Promise.allSettled([p1, p2]): NEVER rejects early. Waits for all to complete.
// Returns array of objects: { status: 'fulfilled', value } or { status: 'rejected', reason }
Promise.allSettled([fetchUsers(), fetchAnalytics()])
  .then(results => results.forEach(res => console.log(res.status)));

// 3. Promise.race([p1, p2]): Resolves OR rejects as soon as the FIRST promise settles.
// Ideal for network timeouts:
Promise.race([
  fetchData(),
  new Promise((_, reject) => setTimeout(() => reject(new Error("Timeout")), 5000))
]);

// 4. Promise.any([p1, p2]): Resolves as soon as the FIRST promise FULFILLS (ignores rejections).
// Rejects with AggregateError only if ALL reject.
```

---

## 2. React & React Native Intermediate

### Q2.11: `useRef` Complete Guide: DOM Reference vs Mutable Instance Values
**Question:** What are the two primary use cases of `useRef` in React? How does it differ from `useState`?

**Answer:**
- `useRef(initialValue)` returns a mutable object `{ current: initialValue }` whose reference persists across renders.
- **Key Difference**: Mutating `.current` does **NOT trigger a component re-render**.

**Use Cases:**
1. **Accessing & Manipulating DOM Nodes**: Direct focus, canvas drawing, measuring element sizes.
2. **Storing Mutable Values Across Renders**: Storing interval IDs, previous state snapshots, request counters.

```jsx
function TimerComponent() {
  const [seconds, setSeconds] = useState(0);
  const timerRef = useRef(null); // Stores interval ID without re-rendering
  const inputRef = useRef(null); // Direct DOM access

  const startTimer = () => {
    if (timerRef.current !== null) return;
    timerRef.current = setInterval(() => {
      setSeconds(prev => prev + 1);
    }, 1000);
  };

  const stopTimer = () => {
    clearInterval(timerRef.current);
    timerRef.current = null;
  };

  const focusInput = () => {
    inputRef.current.focus(); // Focus input directly
  };

  return (
    <div>
      <input ref={inputRef} placeholder="Focus me..." />
      <button onClick={focusInput}>Focus</button>
      <h2>Seconds: {seconds}</h2>
      <button onClick={startTimer}>Start</button>
      <button onClick={stopTimer}>Stop</button>
    </div>
  );
}
```

---

### Q2.12: React Performance Optimization: `React.memo`, `useMemo`, `useCallback`, Code Splitting
**Question:** How do you diagnose and optimize re-render performance in a large-scale React application?

**Answer:**
1. **`React.memo`**: Higher-Order Component that skips re-rendering a child component if its props have not changed (shallow prop comparison).
2. **`useMemo`**: Caches the *result of an expensive computation* across renders unless specified dependencies change.
3. **`useCallback`**: Caches a *function instance reference* across renders to prevent unnecessary re-renders of `React.memo`-wrapped child components that receive callbacks as props.
4. **Code Splitting (`React.lazy` & `Suspense`)**: Splits large bundle sizes into on-demand asynchronous chunks loaded only when route is visited.
5. **Windowing / Virtualization**: Rendering only visible rows in huge lists (e.g., `react-window`).

```jsx
import React, { useState, useMemo, useCallback } from 'react';

// Memoized child component
const UserItem = React.memo(({ user, onDelete }) => {
  console.log("Rendered UserItem:", user.name);
  return (
    <div>
      <span>{user.name}</span>
      <button onClick={() => onDelete(user.id)}>Delete</button>
    </div>
  );
});

function UserListApp({ users }) {
  const [search, setSearch] = useState("");

  // 1. useMemo: Caches filtered array calculation
  const filteredUsers = useMemo(() => {
    return users.filter(u => u.name.toLowerCase().includes(search.toLowerCase()));
  }, [users, search]);

  // 2. useCallback: Preserves reference of onDelete so UserItem doesn't re-render
  const handleDelete = useCallback((id) => {
    console.log("Delete user:", id);
  }, []);

  return (
    <div>
      <input value={search} onChange={e => setSearch(e.target.value)} />
      {filteredUsers.map(user => (
        <UserItem key={user.id} user={user} onDelete={handleDelete} />
      ))}
    </div>
  );
}
```

---

### Q2.13: Cross-Origin Resource Sharing (CORS): Preflight, Headers & Express Config
**Question:** What causes CORS errors, what is a Preflight `OPTIONS` request, and how do you resolve CORS properly on an Express backend?

**Answer:**
**CORS** is a browser security mechanism that blocks web pages running on one origin (e.g., `http://localhost:3000`) from making HTTP requests to a different origin (e.g., `http://api.myapp.com`) unless the server explicitly grants permission via HTTP response headers.

**Preflight Request (`OPTIONS`)**:
For "non-simple" requests (requests with `PUT`, `DELETE`, `PATCH`, custom headers like `Authorization: Bearer <token>`, or `Content-Type: application/json`), the browser automatically sends an HTTP `OPTIONS` preflight request first to check server permissions.

```javascript
// Express.js Backend Solution
const express = require('express');
const cors = require('cors');
const app = express();

// Secure CORS Configuration
const allowedOrigins = ['https://myapp.com', 'http://localhost:3000'];

app.use(cors({
  origin: function (origin, callback) {
    // Allow requests with no origin (like mobile apps or curl)
    if (!origin || allowedOrigins.includes(origin)) {
      callback(null, true);
    } else {
      callback(new Error('Blocked by CORS policy'));
    }
  },
  methods: ['GET', 'POST', 'PUT', 'DELETE', 'PATCH', 'OPTIONS'],
  allowedHeaders: ['Content-Type', 'Authorization'],
  credentials: true // Allow cookies / authorization headers
}));
```

---

### Q2.14: React Native: `ScrollView` vs `FlatList` vs `SafeAreaView` vs `map()`
**Question:** Compare `ScrollView`, `FlatList`, `SafeAreaView`, and `Array.map()` in React Native.

**Answer:**
| Component | Rendering Mechanism | Memory Usage for 10,000 Items | Use Case |
| :--- | :--- | :--- | :--- |
| `ScrollView` | Renders **all** child components simultaneously into native views on initial load. | ❌ Extremely High (Crashes App) | Small, fixed content forms, settings pages (< 30 items). |
| `FlatList` | **Virtualized Lazy Loading**: Only renders items currently visible in the viewport (+ small buffer). Unmounts off-screen items. | ✅ Constant / Low ($O(1)$ visible items) | Large or infinite lists, chat feeds, product catalogs. |
| `Array.map()` | Raw JS iteration without built-in scrolling behavior. | High if inside ScrollView | Small inline button groups or static tags. |
| `SafeAreaView` | Renders content within safe area boundaries (avoids notches, status bars, and home indicators). | N/A (Layout wrapper) | Root screen container for iOS & Android devices. |

---

### Q2.15: Horizontal Scrolling Implementation in React Native & CSS
**Question:** How do you implement horizontal scrolling in React Native and Vanilla CSS?

**Answer:**
```jsx
// React Native Implementation
import React from 'react';
import { FlatList, View, Text, StyleSheet } from 'react-native';

const categories = ['Tech', 'Design', 'Marketing', 'Finance', 'Crypto', 'AI'];

export const HorizontalCategoryList = () => (
  <FlatList
    horizontal={true}
    showsHorizontalScrollIndicator={false}
    data={categories}
    keyExtractor={(item) => item}
    renderItem={({ item }) => (
      <View style={styles.card}>
        <Text style={styles.text}>{item}</Text>
      </View>
    )}
  />
);

const styles = StyleSheet.create({
  card: {
    paddingHorizontal: 20,
    paddingVertical: 10,
    marginRight: 12,
    backgroundColor: '#007AFF',
    borderRadius: 20
  },
  text: { color: '#fff', fontWeight: 'bold' }
});
```

```css
/* Vanilla CSS Implementation */
.horizontal-scroll-container {
  display: flex;
  overflow-x: auto;
  overflow-y: hidden;
  white-space: nowrap;
  scroll-snap-type: x mandatory;
  -webkit-overflow-scrolling: touch;
  gap: 16px;
  padding: 12px;
}

.scroll-item {
  flex: 0 0 200px; /* Do not shrink or grow, fixed 200px */
  scroll-snap-align: start;
}
```

---

## 3. Node.js, Express, Databases & Redis

### Q2.16: Express Middleware Architecture & The BATER Types
**Question:** What is Express middleware? Explain the **BATER** categorization of middleware.

**Answer:**
Middleware functions are functions that have access to the request object (`req`), response object (`res`), and the `next` function in the application’s request-response cycle.

**BATER Mnemonic for Express Middleware Types:**
1. **B - Built-in Middleware**: Ships natively with Express (e.g., `express.json()`, `express.urlencoded()`, `express.static('public')`).
2. **A - Application-Level Middleware**: Bound directly to an instance of `app` using `app.use()` or `app.get()` (e.g., authentication, request logging).
3. **T - Third-Party Middleware**: Installed via npm (e.g., `cors()`, `helmet()`, `morgan()`, `cookie-parser`).
4. **E - Error-Handling Middleware**: Defined with **4 arguments** `(err, req, res, next)`. Express recognizes this signature specifically for catching errors.
5. **R - Router-Level Middleware**: Bound to an instance of `express.Router()` (e.g., `userRouter.use(authCheck)`).

```javascript
// Example: Complete BATER Implementation
const express = require('express');
const app = express();
const router = express.Router();

// 1. Built-in
app.use(express.json());

// 2. Application-Level
app.use((req, res, next) => {
  console.log(`[${new Date().toISOString()}] ${req.method} ${req.url}`);
  next();
});

// 3. Router-Level
router.use((req, res, next) => {
  if (!req.headers.authorization) return next(new Error("Unauthorized"));
  next();
});
router.get('/profile', (req, res) => res.send("User Profile"));
app.use('/api', router);

// 4. Error-Handling Middleware (Must have 4 parameters)
app.use((err, req, res, next) => {
  console.error("Global Error Caught:", err.message);
  res.status(500).json({ error: true, message: err.message });
});
```

---

### Q2.17: JWT (JSON Web Token) Complete Authentication & Token Refresh Flow
**Question:** Explain the 3 parts of a JWT and the secure Access Token + Refresh Token rotation workflow.

**Answer:**
A JWT consists of 3 Base64URL-encoded parts separated by dots:
`Header.Payload.Signature`
- **Header**: Token type (`JWT`) and signing algorithm (`HS256` or `RS256`).
- **Payload**: Claims (e.g., `userId`, `role`, expiration `exp`). *Not encrypted*, only encoded!
- **Signature**: `HMACSHA256(base64Url(header) + "." + base64Url(payload), secretKey)` to prevent tampering.

```
+-----------+                +--------------+                     +---------------+
|  Client   |                | Auth Server  |                     | Resource API  |
+-----------+                +--------------+                     +---------------+
      |                             |                                     |
      | 1. Login (Email + Pass)     |                                     |
      |---------------------------->|                                     |
      | 2. Returns Short-Lived      |                                     |
      |    AccessToken (15m in Mem) |                                     |
      |    + RefreshToken (HttpOnly)|                                     |
      |<----------------------------|                                     |
      |                                                                   |
      | 3. API Request (Bearer AccessToken)                               |
      |------------------------------------------------------------------>|
      | 4. AccessToken Expired (401 Unauthorized)                         |
      |<------------------------------------------------------------------|
      |                                                                   |
      | 5. POST /refresh (Send HttpOnly RefreshToken Cookie)              |
      |---------------------------->|                                     |
      | 6. Validate & Rotate Token  |                                     |
      |    Returns new AccessToken  |                                     |
      |<----------------------------|                                     |
```

---

### Q2.18: Why is `bcrypt` Used for Password Hashing Instead of SHA-256?
**Question:** Why are fast cryptographic hashes like SHA-256 or MD5 vulnerable for password storage, and why is `bcrypt` preferred?

**Answer:**
1. **Speed Vulnerability**: SHA-256 is designed to be extremely fast for file verification and data integrity. Modern GPUs can calculate billions of SHA-256 hashes per second, making offline brute-force and dictionary attacks trivial.
2. **Key Stretching & Work Factor (Cost Factor)**: `bcrypt` incorporates an adaptive work factor (`saltRounds`, e.g., 10-12). As hardware becomes faster, developers can increase the work factor to make hashing intentionally computationally expensive and slow down attackers.
3. **Automatic Unique Salt**: `bcrypt` automatically generates and embeds a random 128-bit salt inside the resulting hash string, preventing Rainbow Table attacks.

```javascript
const bcrypt = require('bcrypt');

async function hashPassword(password) {
  const saltRounds = 12; // 2^12 iterations
  return await bcrypt.hash(password, saltRounds);
}

async function verifyPassword(password, hash) {
  return await bcrypt.compare(password, hash);
}
```

---

### Q2.19: API Rate Limiting: Fixed Window vs Token Bucket Algorithms
**Question:** What is API Rate Limiting, and how does the Token Bucket algorithm work?

**Answer:**
Rate limiting controls the rate of incoming requests sent to a server to prevent denial-of-service (DoS) attacks, brute-force login attempts, and resource starvation.

- **Fixed Window Counter**: Divides time into fixed windows (e.g., 1 minute). Counts requests per window. *Flaw*: A traffic burst at window boundaries (last second of minute 1 and first second of minute 2) can send 2x the allowed limit.
- **Token Bucket Algorithm**: A bucket holds up to $B$ tokens. Tokens are continuously added at a constant rate $R$ per second. When a request arrives, it consumes 1 token. If the bucket is empty, the request is rejected (`429 Too Many Requests`). Allows bursts of up to $B$ requests while enforcing average rate $R$.

---

### Q2.20: MongoDB `populate()` & Query Filtering Within Nested Populates
**Question:** How does Mongoose `populate()` work under the hood? Show how to filter and sort inside nested populates.

**Answer:**
MongoDB is a non-relational database and does not natively execute relational SQL `JOIN` operations inside the database engine. In Mongoose, `populate()` performs a **secondary batch query** behind the scenes (`db.orders.find({ _id: { $in: [...] } })`) and joins the documents in Node.js application memory.

```javascript
// Advanced Query Filtering & Nested Population
const User = require('../models/User');

async function getUserOrderDetails(userId) {
  return await User.findById(userId)
    .populate({
      path: 'orders',
      match: { status: 'DELIVERED', totalAmount: { $gte: 100 } }, // Filter inside populated collection
      select: 'totalAmount createdAt items',
      options: { sort: { createdAt: -1 }, limit: 5 }, // Sort and paginate populated docs
      populate: {
        path: 'items.product', // Nested population
        select: 'name price category'
      }
    })
    .exec();
}
```

---

### Q2.21: Compound Indexing in Databases & The ESR (Equality, Sort, Range) Rule
**Question:** What is a Compound Index? Explain the **ESR Rule** for designing optimal compound indexes.

**Answer:**
A **Compound Index** indexes multiple fields within a single B-tree index structure. The order of fields in the index definition is critical.

**The ESR (Equality, Sort, Range) Rule:**
When constructing a compound index for complex queries:
1. **E - Equality**: Place fields queried with exact equality match (`status: "ACTIVE"`) **first**.
2. **S - Sort**: Place fields used for ordering (`sort: { createdAt: -1 }`) **second**.
3. **R - Range**: Place fields queried with range operators (`$gt`, `$lt`, `$in`, `$gte`) **last**.

```javascript
// Query Example:
// db.orders.find({ status: "PAID", total: { $gte: 500 } }).sort({ createdAt: -1 })

// Optimal Index according to ESR Rule:
// 1. Equality: 'status'
// 2. Sort:     'createdAt'
// 3. Range:    'total'
db.orders.createIndex({ status: 1, createdAt: -1, total: 1 });
```

---

### Q2.22: Redis Caching Architecture & Why It Is Not Always Used in Small Projects
**Question:** Explain common Redis use cases. Why do many small-to-medium projects avoid using Redis?

**Answer:**
**Primary Redis Use Cases:**
1. **In-Memory Caching**: Cache expensive DB query results with TTL (Time-To-Live).
2. **Session Storage**: Fast, centralized user session storage across load-balanced Node servers.
3. **Distributed Locks**: Redlock algorithm for coordinating concurrency across microservices.
4. **Pub/Sub & Message Queues**: Real-time message broadcasting and background task queuing (BullMQ).
5. **Rate Limiter Counters**: Fast atomic increment operations (`INCR`, `EXPIRE`).

**Why Redis Is Avoided in Many Small/Medium Projects:**
1. **RAM Cost**: Redis stores everything entirely in RAM, which is significantly more expensive per GB than SSD disk storage.
2. **Architectural Complexity**: Introduces cache invalidation challenges ("Cache Invalidation is one of the hardest problems in CS"), cache stampede, and cache penetration issues.
3. **Data Loss Risk**: Redis is an in-memory store; while it supports persistence (RDB snapshots and AOF logs), it is not designed as a primary durable ACID database.
4. **Infrastructure Overhead**: Requires maintaining a separate cluster, backup policies, failover nodes, and memory monitoring.

---

## 4. DSA Medium

### Q2.23: Valid Parentheses (Stack)
**Problem:** Given a string containing `'('`, `')'`, `'{'`, `'}'`, `'['`, `']'`, determine if the input string is valid.

```javascript
// Time Complexity: O(N), Space Complexity: O(N)
function isValid(s) {
  const stack = [];
  const map = {
    ')': '(',
    '}': '{',
    ']': '['
  };

  for (const char of s) {
    if (char === '(' || char === '{' || char === '[') {
      stack.push(char);
    } else if (map[char]) {
      if (stack.pop() !== map[char]) {
        return false;
      }
    }
  }

  return stack.length === 0;
}

console.log(isValid("({[]})")); // true
console.log(isValid("([)]"));   // false
```

---

### Q2.24: Happy Number (Floyd's Cycle-Finding Algorithm)
**Problem:** A happy number is a number defined by replacing the number with the sum of the squares of its digits repeatedly until it equals 1, or it loops endlessly in a cycle.

```javascript
// Time Complexity: O(log N), Space Complexity: O(1)
function isHappy(n) {
  function getNext(num) {
    let totalSum = 0;
    while (num > 0) {
      let d = num % 10;
      totalSum += d * d;
      num = Math.floor(num / 10);
    }
    return totalSum;
  }

  // Floyd's Tortoise and Hare Cycle Detection
  let slow = n;
  let fast = getNext(n);

  while (fast !== 1 && slow !== fast) {
    slow = getNext(slow);
    fast = getNext(getNext(fast));
  }

  return fast === 1;
}

console.log(isHappy(19)); // true (1^2 + 9^2 = 82 -> 8^2 + 2^2 = 68 -> ... -> 1)
console.log(isHappy(2));  // false (enters cycle)
```

---

### Q2.25: Two Sum (Optimal Hash Map O(N))
**Problem:** Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`.

```javascript
// Time Complexity: O(N), Space Complexity: O(N)
function twoSum(nums, target) {
  const seen = new Map(); // value -> index

  for (let i = 0; i < nums.length; i++) {
    const complement = target - nums[i];
    if (seen.has(complement)) {
      return [seen.get(complement), i];
    }
    seen.set(nums[i], i);
  }
  return [];
}

console.log(twoSum([2, 7, 11, 15], 9)); // [0, 1]
```

---

### Q2.26: Fibonacci Sequence (Iterative, Recursive, Dynamic Programming)
**Problem:** Compute the $N$-th Fibonacci number with optimal space and time.

```javascript
// 1. Recursive: O(2^N) Time, O(N) Call Stack
function fibRecursive(n) {
  if (n <= 1) return n;
  return fibRecursive(n - 1) + fibRecursive(n - 2);
}

// 2. Memoized DP (Top-Down): O(N) Time, O(N) Space
function fibMemo(n, memo = {}) {
  if (n in memo) return memo[n];
  if (n <= 1) return n;
  return (memo[n] = fibMemo(n - 1, memo) + fibMemo(n - 2, memo));
}

// 3. Iterative Space-Optimized (Bottom-Up): O(N) Time, O(1) Space
function fibOptimal(n) {
  if (n <= 1) return n;
  let prev2 = 0, prev1 = 1;
  for (let i = 2; i <= n; i++) {
    let current = prev1 + prev2;
    prev2 = prev1;
    prev1 = current;
  }
  return prev1;
}
```

---

### Q2.27: Rotate Array by K Positions (Reversal Algorithm O(1) Space)
**Problem:** Rotate an array of $N$ elements to the right by $K$ steps in $O(N)$ time and $O(1)$ auxiliary space.

```javascript
function rotateArray(nums, k) {
  k = k % nums.length; // Handle k > length

  function reverse(arr, start, end) {
    while (start < end) {
      [arr[start], arr[end]] = [arr[end], arr[start]];
      start++;
      end--;
    }
  }

  // 1. Reverse entire array
  reverse(nums, 0, nums.length - 1);
  // 2. Reverse first k elements
  reverse(nums, 0, k - 1);
  // 3. Reverse remaining elements
  reverse(nums, k, nums.length - 1);

  return nums;
}

console.log(rotateArray([1, 2, 3, 4, 5, 6, 7], 3)); // [5, 6, 7, 1, 2, 3, 4]
```

---

### Q2.28: Sliding Window Technique: Maximum Sum Subarray of Size K
**Problem:** Find maximum sum of any contiguous subarray of size $K$.

```javascript
// Time Complexity: O(N), Space Complexity: O(1)
function maxSubarraySum(arr, k) {
  if (arr.length < k) return null;

  let maxSum = 0;
  let windowSum = 0;

  // Calculate sum of initial window
  for (let i = 0; i < k; i++) {
    windowSum += arr[i];
  }
  maxSum = windowSum;

  // Slide window across remaining array
  for (let i = k; i < arr.length; i++) {
    windowSum += arr[i] - arr[i - k]; // Add incoming, subtract outgoing
    maxSum = Math.max(maxSum, windowSum);
  }

  return maxSum;
}

console.log(maxSubarraySum([2, 1, 5, 1, 3, 2], 3)); // 9 (Subarray [5, 1, 3])
```

---

# 🔴 Level 3: HARD (Advanced Engine Internals, Concurrency & Low-Level Architecture)

---

## 1. JavaScript & Engine Deep Internals

### Q3.1: Complete Execution Breakdown of the `this` Keyword Across 6 Contexts
**Question:** Explain how `this` is evaluated in JavaScript across all execution contexts.

**Answer:**
`this` is not static; it is determined dynamically by **how a function is invoked**:

```javascript
// 1. Global Context
console.log(this); // Browser: window | Node.js: module.exports {}

// 2. Function Call (Non-strict vs Strict mode)
function showThis() { return this; }
console.log(showThis()); // Non-strict: window/global | Strict ('use strict'): undefined

// 3. Object Method Call (Implicit Binding)
const obj = {
  name: "Master Guide",
  getName() { return this.name; }
};
console.log(obj.getName()); // "Master Guide" (Points to calling object 'obj')

const detached = obj.getName;
// console.log(detached()); // undefined / Error (Lost implicit binding)

// 4. Explicit Binding (call, apply, bind)
function greet() { return `Hello, ${this.user}`; }
console.log(greet.call({ user: "Utkarsh" })); // "Hello, Utkarsh"

// 5. Constructor Call (new keyword)
function User(name) {
  // 'new' creates new object {} and binds 'this' to it
  this.name = name;
}
const u = new User("Alex");
console.log(u.name); // "Alex"

// 6. Arrow Functions (Lexical Binding)
const group = {
  title: "Engineering",
  members: ["A", "B"],
  printMembers() {
    this.members.forEach((m) => {
      // Arrow function captures 'this' from printMembers (the group object)
      console.log(`${m} is in ${this.title}`);
    });
  }
};
group.printMembers();
```

---

## 2. Node.js Engine, Concurrency & React Native Architecture

### Q3.2: Libuv Architecture: Event Loop Phases & Thread Pool (`UV_THREADPOOL_SIZE`)
**Question:** Explain the internal architecture of Libuv, the 6 phases of the Node.js Event Loop, and how the background Thread Pool operates.

**Answer:**
Libuv is a multi-platform C library providing Node.js with asynchronous I/O based on an event-driven loop and a worker thread pool.

```
   ┌───────────────────────────┐
┌─>│          timers           │  -> Executes callbacks from setTimeout() & setInterval()
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │     pending callbacks     │  -> Executes I/O callbacks deferred from previous loop
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │       idle, prepare       │  -> Used internally by Libuv only
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │           poll            │  -> Retrieves new I/O events; executes I/O related callbacks
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │           check           │  -> Executes callbacks from setImmediate()
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │      close callbacks      │  -> Executes close events, e.g. socket.on('close', ...)
└──┴───────────────────────────┘
```

**The Libuv Thread Pool:**
Node's JavaScript executes on a single main thread. However, blocking operations are offloaded by Libuv to a background worker thread pool.
- **Offloaded Operations**: `fs` (File System operations), `crypto` (Hashing, PBKDF2, randomBytes), `zlib` (Compression), and DNS lookup (`dns.lookup`).
- **Network I/O (HTTP/TCP/Sockets)**: Handled directly by operating system kernel asynchronous mechanisms (`epoll` on Linux, `kqueue` on macOS, `IOCP` on Windows), **without** using the thread pool.
- **Thread Pool Size**: Defaults to **4 threads**. Can be adjusted up to 1024 before application starts:
  ```bash
  UV_THREADPOOL_SIZE=8 node server.js
  ```

---

### Q3.3: Microtasks vs Macrotasks: `process.nextTick()` vs `setImmediate()` vs `setTimeout()`
**Question:** Explain the execution order of `process.nextTick()`, `Promise.then()`, `setTimeout()`, and `setImmediate()`.

**Answer:**
1. **Microtask Queue**:
   - `process.nextTick()` queue has the **highest priority**; it drains immediately after the current operation finishes, before any other microtask or event loop phase.
   - `Promise` microtask queue (`Promise.then`, `queueMicrotask`) executes immediately after `nextTick`.
2. **Macrotask Queue**:
   - `setTimeout(fn, 0)` is evaluated in the **Timers phase**.
   - `setImmediate(fn)` is evaluated in the **Check phase**.

```javascript
console.log("1. Sync Main Start");

setTimeout(() => {
  console.log("6. setTimeout (Macrotask: Timers Phase)");
}, 0);

setImmediate(() => {
  console.log("7. setImmediate (Macrotask: Check Phase)");
});

Promise.resolve().then(() => {
  console.log("4. Promise.then (Microtask)");
});

process.nextTick(() => {
  console.log("3. process.nextTick (Microtask: Priority 1)");
});

queueMicrotask(() => {
  console.log("5. queueMicrotask (Microtask)");
});

console.log("2. Sync Main End");

// Output Order:
// 1. Sync Main Start
// 2. Sync Main End
// 3. process.nextTick (Microtask: Priority 1)
// 4. Promise.then (Microtask)
// 5. queueMicrotask (Microtask)
// 6. setTimeout (Macrotask: Timers Phase)
// 7. setImmediate (Macrotask: Check Phase)
```

---

### Q3.4: Node.js Buffer Internals & Raw Binary Memory Management
**Question:** What is a Buffer in Node.js, where is it allocated in memory, and how do you manipulate binary streams?

**Answer:**
A `Buffer` represents a fixed-length sequence of raw binary bytes allocated **outside the V8 JavaScript garbage-collected heap** directly in raw memory (via C++ Libuv layer). This prevents V8 GC pauses when dealing with large files, images, or network payloads.

```javascript
// Allocates 10 bytes filled with zeros in raw memory outside V8
const buf = Buffer.alloc(10);

// Unsafe fast allocation (does not zero-out memory; contains old memory garbage)
const unsafeBuf = Buffer.allocUnsafe(10);

// Creating buffer from UTF-8 string
const strBuf = Buffer.from("FullStack", "utf-8");
console.log(strBuf); // <Buffer 46 75 6c 6c 53 74 61 63 6b> (Hex representation)
console.log(strBuf.toString("hex")); // "46756c6c537461636b"
console.log(strBuf.toString("base64")); // "RnVsbFN0YWNr"
```

---

### Q3.5: Node.js Streams: Readable, Writable, Duplex, Transform, Piping & Backpressure
**Question:** Explain the 4 types of Node.js Streams. What is **Backpressure**, and how does `.pipe()` or `pipeline()` prevent memory crashes?

**Answer:**
**The 4 Stream Types:**
1. **Readable**: Source from which data can be consumed (e.g., `fs.createReadStream()`, `req` in HTTP).
2. **Writable**: Destination to which data can be written (e.g., `fs.createWriteStream()`, `res` in HTTP).
3. **Duplex**: Stream that is both Readable and Writable (e.g., `net.Socket`).
4. **Transform**: Duplex stream that modifies data as it is read and written (e.g., `zlib.createGzip()`, `crypto.createCipher()`).

**What is Backpressure?**
Backpressure occurs when the **data producer (Readable stream) reads faster than the data consumer (Writable stream) can write to disk or network**. If unmanaged, incoming chunks accumulate in RAM buffers until the Node.js process crashes with `JavaScript heap out of memory`.

```javascript
const fs = require('fs');
const zlib = require('zlib');
const { pipeline } = require('stream/promises'); // Handles backpressure & cleanup automatically

async function compressLargeFile(sourcePath, destinationPath) {
  try {
    await pipeline(
      fs.createReadStream(sourcePath),  // Readable
      zlib.createGzip(),                 // Transform
      fs.createWriteStream(destinationPath) // Writable (Backpressure handled)
    );
    console.log("Streaming compression complete!");
  } catch (err) {
    console.error("Pipeline failed:", err);
  }
}
```

---

### Q3.6: File Systems, Streams & Threading: Node.js vs React Native Bridge/JSI Architecture
**Question:** Compare how File Systems (`fs`), Streams, and Threading are handled in Node.js vs React Native.

**Answer:**
| Architecture Domain | Node.js | React Native (Architecture) |
| :--- | :--- | :--- |
| **Execution Environment** | Single V8 instance on top of Libuv C/C++ backend. | Mobile JavaScript engine (Hermes / JSC) running on a dedicated JS Thread. |
| **File System (`fs`)** | Built-in `fs` and `fs/promises` module reading directly from OS disk via Libuv thread pool. | No built-in `fs`. Requires native third-party modules (`react-native-fs`, `expo-file-system`) interacting over the native boundary. |
| **Threading Model** | Main JS Thread + Libuv Thread Pool + `worker_threads` for parallel JS execution. | **3 Core Threads**:<br>1. **JS Thread**: Runs React component code.<br>2. **UI Main Thread**: Manages native UI views and touch gestures.<br>3. **Shadow Thread**: Calculates layout using Yoga engine. |
| **Communication Bridge** | Direct C++ internal bindings (nan / N-API). | **Old Architecture**: Asynchronous JSON serialization over the asynchronous Bridge.<br>**New Architecture (JSI)**: Direct synchronous C++ memory references using JavaScript Interface (JSI). |

---

### Q3.7: Multi-Process Concurrency: Node.js `cluster` Module & Worker Threads
**Question:** When should you use the `cluster` module vs `worker_threads` in Node.js?

**Answer:**
- **`cluster` Module (Multi-Process)**: Forks multiple instances of the Node.js process (one per CPU core) that share the same server port. Used to scale I/O-bound web servers horizontally across multi-core systems. Memory is **isolated** between processes.
- **`worker_threads` Module (Multi-Threaded JS)**: Runs multiple threads within a **single process**. Threads can share memory using `SharedArrayBuffer`. Used for CPU-intensive tasks (image processing, video transcoding, heavy cryptography, machine learning calculations) without blocking the main event loop.

```javascript
// Horizontal Scaling with Node.js Cluster
const cluster = require('cluster');
const http = require('http');
const os = require('os');

if (cluster.isPrimary) {
  const numCPUs = os.cpus().length;
  console.log(`Primary master ${process.pid} is running. Forking ${numCPUs} workers...`);

  for (let i = 0; i < numCPUs; i++) {
    cluster.fork();
  }

  cluster.on('exit', (worker, code, signal) => {
    console.log(`Worker ${worker.process.pid} died. Forking replacement worker...`);
    cluster.fork();
  });
} else {
  // Worker processes share the TCP connection on port 8000
  http.createServer((req, res) => {
    res.writeHead(200);
    res.end(`Handled by worker PID: ${process.pid}\n`);
  }).listen(8000);

  console.log(`Worker ${process.pid} started.`);
}
```

---

## 🎯 Summary Checklist for Technical Interviews

| Category | Must-Master Concepts |
| :--- | :--- |
| **HTML / CSS** | Semantic tags, `async`/`defer`, `href` vs `src`, CSS Box Model, Flexbox vs Grid, Positioning rules. |
| **JavaScript Core** | Closures, Prototype chain, `this` binding, Hoisting & TDZ, Event Loop, Microtasks vs Macrotasks, Debounce/Throttle. |
| **React & Native** | Hook rules, `useState` batching, `useEffect` dependencies, `useRef`, Memoization (`React.memo`, `useMemo`, `useCallback`), `FlatList` virtualization. |
| **Backend & Node** | Libuv architecture, Event loop phases, Streams & Backpressure, Middleware BATER, JWT rotation, bcrypt work factor. |
| **Databases** | SQL vs NoSQL, B-Tree indexes, Compound Index ESR rule, Mongoose `populate` mechanics, Redis caching strategies. |
| **DSA & Problem Solving** | Stack parsing, Two Pointers, Fast & Slow pointers, Sliding Window, Bitwise XOR operations, Space optimization. |