# 📜 JavaScript - Easy Questions From Notes

> **Topics from Notes Covered:** `var`/`let`/`const` diff, Hoisting, TDZ, Data Types in JS (`dt in js`), Keywords in JS, Spread vs Rest operator, Destructuring, ES6 features, Substring vs Slice, DOM APIs (`getElementById`, `createElement`, `innerHTML`, `innerText`, `textContent`), `e.preventDefault`, Pure Functions, How to write Arrow Functions.

---

### Q1: `var` vs `let` vs `const`, Hoisting & Temporal Dead Zone (TDZ)
**Question (From Notes):** What is the difference between `var`, `let`, and `const`? Explain Hoisting and TDZ.

**Answer:**
| Feature | `var` | `let` | `const` |
| :--- | :--- | :--- | :--- |
| **Scope** | Function Scope | Block Scope (`{}`) | Block Scope (`{}`) |
| **Hoisting** | Hoisted & initialized to `undefined` | Hoisted but placed in **TDZ** | Hoisted but placed in **TDZ** |
| **Re-declaration** | Allowed in same scope | Throws `SyntaxError` | Throws `SyntaxError` |
| **Re-assignment** | Allowed | Allowed | Throws `TypeError` |

**Temporal Dead Zone (TDZ):**
The time window between entering a block scope and the variable declaration being evaluated. Accessing a `let` or `const` variable in its TDZ throws a `ReferenceError`.

```javascript
console.log(a); // undefined (hoisted & initialized)
// console.log(b); // ReferenceError: Cannot access 'b' before initialization (in TDZ)

var a = 10;
let b = 20; // TDZ for 'b' ends here
```

---

### Q2: Data Types in JavaScript (`dt in js`) & Primitive vs Reference Types
**Question (From Notes):** What are the data types in JavaScript? Explain Primitive vs Reference types.

**Answer:**
- **7 Primitive Data Types** (Stored directly in **Stack**, immutable by value):
  1. `string`
  2. `number`
  3. `bigint`
  4. `boolean`
  5. `undefined`
  6. `symbol`
  7. `null`
- **Reference Types** (Stored in **Heap**, variable holds stack pointer):
  `Object`, `Array`, `Function`, `Date`, `Map`, `Set`.

```javascript
// Primitive: Pass-by-value
let x = 10;
let y = x;
y = 20;
console.log(x); // 10 (unchanged)

// Reference: Pass-by-reference
let obj1 = { name: "Utkarsh" };
let obj2 = obj1;
obj2.name = "Alex";
console.log(obj1.name); // "Alex" (mutates shared heap data)
```

---

### Q3: Keywords in JavaScript
**Question (From Notes):** What are keywords in JavaScript?

**Answer:**
Keywords are reserved words that have predefined special meaning in JavaScript syntax and cannot be used as variable or function names (e.g., `var`, `let`, `const`, `function`, `return`, `if`, `else`, `for`, `while`, `class`, `this`, `new`, `typeof`, `instanceof`, `try`, `catch`, `async`, `await`, `import`, `export`).

---

### Q4: Spread Operator (`...`) vs Rest Operator (`...`)
**Question (From Notes):** Differentiate between Spread and Rest operators.

**Answer:**
- **Spread Operator**: Unpacks / expands elements of an array or object.
- **Rest Operator**: Gathers / condenses multiple parameters into a single array structure.

```javascript
// Rest: In function parameters
function sumAll(...numbers) {
  return numbers.reduce((acc, n) => acc + n, 0);
}
console.log(sumAll(1, 2, 3, 4)); // 10

// Spread: In array/object cloning and merging
const arr1 = [1, 2];
const arr2 = [...arr1, 3, 4]; // [1, 2, 3, 4]
```

---

### Q5: Destructuring (Arrays & Objects)
**Question (From Notes):** Explain Array and Object destructuring.

```javascript
// Array Destructuring
const [first, second, ...rest] = [10, 20, 30, 40];

// Object Destructuring with Rename & Default
const user = { username: "utkarsh", role: "admin" };
const { username: name, role, status = "active" } = user;
console.log(name, role, status); // "utkarsh", "admin", "active"
```

---

### Q6: Core ES6 Features Overview
**Question (From Notes):** What are the key ES6 (ECMAScript 2015) features?

**Answer:**
1. `let` and `const` (Block-scoped variables).
2. Arrow functions (`() => {}`).
3. Template literals (`` `Hello ${name}` ``).
4. Destructuring (Array and Object).
5. Spread and Rest operators (`...`).
6. Default parameters (`function fn(x = 10)`).
7. Classes and Modules (`import` / `export`).
8. Promises (`new Promise()`).

---

### Q7: String Slicing: `substring` vs `substr` vs `slice`
**Question (From Notes):** How does `substring` work compared to `substr` and `slice`?

**Answer:**
| Method | Negative Index Support | Argument Swapping (`start > end`) | Status |
| :--- | :--- | :--- | :--- |
| `slice(start, end)` | ✅ Counts from end of string | ❌ Returns `""` | Standard |
| `substring(start, end)` | ❌ Treats negative as `0` | ✅ Swaps arguments if `start > end` | Standard |
| `substr(start, length)` | ✅ Negative start allowed | N/A (second arg is length) | ⚠️ Deprecated |

```javascript
const str = "JavaScript";
console.log(str.slice(-6));       // "Script"
console.log(str.substring(4, 0)); // "Java" (swaps 4 and 0)
```

---

### Q8: DOM Manipulation: `getElementById`, `createElement`, `innerHTML`, `innerText`, `textContent`
**Question (From Notes):** Compare `innerHTML`, `innerText`, and `textContent`.

**Answer:**
- `getElementById`: Selects DOM element by unique ID.
- `createElement`: Creates a new HTML element node.
- `innerHTML`: Parses and inserts raw HTML markup. ⚠️ Risk of XSS vulnerability.
- `innerText`: Returns only visible rendered text. Triggers layout reflow (respects `display: none`).
- `textContent`: Returns full text content of all nodes including hidden elements. Fast and safe.

```javascript
const container = document.getElementById("root");
const newEl = document.createElement("p");
newEl.textContent = "Safe Text Content";
container.appendChild(newEl);
```

---

### Q9: `e.preventDefault` Method
**Question (From Notes):** What does `e.preventDefault()` do?

**Answer:**
`e.preventDefault()` prevents the **default browser behavior** for an event (e.g., stops `<form>` submission from reloading the page, stops `<a>` links from navigating, or prevents checkbox toggling).

```javascript
document.querySelector("form").addEventListener("submit", (e) => {
  e.preventDefault(); // Prevents page refresh
  console.log("Form submitted via AJAX");
});
```

---

### Q10: Pure Function
**Question (From Notes):** What is a Pure Function?

**Answer:**
A **Pure Function**:
1. Given the same inputs, always returns the exact same output.
2. Produces **no side effects** (does not mutate external state, modify parameters, or perform I/O).

```javascript
// Pure
const add = (a, b) => a + b;

// Impure (Side effect: alters external variable)
let count = 0;
const increment = () => ++count;
```

---

### Q11: How to Write Arrow Functions & Differences with Regular Functions
**Question (From Notes):** How to write Arrow functions, and how do they differ from regular functions?

**Answer:**
```javascript
// Regular Function
function multiplyRegular(a, b) {
  return a * b;
}

// Arrow Function
const multiplyArrow = (a, b) => a * b;
```

**Key Differences:**
1. **`this` Binding**: Arrow functions do not have their own `this`; they capture `this` lexically from their enclosing scope.
2. **`arguments` Object**: Arrow functions do not have an `arguments` object (use rest `...args`).
3. **Constructors**: Arrow functions cannot be called with `new` (throws `TypeError`).
