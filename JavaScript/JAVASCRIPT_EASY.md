# 📜 JavaScript - Easy & Fundamentals

> **Topics Covered:** `var` vs `let` vs `const`, Hoisting & TDZ, Data Types & Memory (Primitive vs Reference, Stack vs Heap), Type Coercion vs Conversion, Truthy & Falsy Values, Destructuring, Spread vs Rest, Object.freeze() vs Object.seal(), Object.keys()/values()/entries(), forEach vs map, Array Manipulation, String Methods, DOM Manipulation (`getElementById`, `createElement`, `innerHTML` vs `innerText` vs `textContent`).

---

### Q1: `var` vs `let` vs `const`, Hoisting & Temporal Dead Zone (TDZ)
**Question:** What are the exact differences between `var`, `let`, and `const`? Explain Hoisting and TDZ.

**Answer:**
| Feature | `var` | `let` | `const` |
| :--- | :--- | :--- | :--- |
| **Scope** | Function Scope | Block Scope (`{}`) | Block Scope (`{}`) |
| **Hoisting** | Hoisted & initialized to `undefined` | Hoisted into **TDZ** | Hoisted into **TDZ** |
| **Re-declaration** | Allowed in same scope | Throws `SyntaxError` | Throws `SyntaxError` |
| **Re-assignment** | Allowed | Allowed | Throws `TypeError` |
| **Global Window Property** | Creates property on `window` | Does not create on `window` | Does not create on `window` |

**Temporal Dead Zone (TDZ):**
The duration between entering scope and variable initialization. Accessing during TDZ throws `ReferenceError`.

```javascript
console.log(a); // undefined
// console.log(b); // ReferenceError: Cannot access 'b' before initialization (in TDZ)

var a = 10;
let b = 20; // TDZ ends here
```

---

### Q2: Primitive vs Reference Data Types (Stack vs Heap)
**Question:** What are the 7 primitive data types versus reference types? How are they stored in memory?

**Answer:**
- **7 Primitive Types** (Stored directly on the **Call Stack**, immutable value, pass-by-value):
  `string`, `number`, `bigint`, `boolean`, `undefined`, `symbol`, `null`.
- **Reference Types** (Stored on the **Heap**, stack variable holds reference pointer, pass-by-reference):
  `Object`, `Array`, `Function`, `Date`, `Map`, `Set`.

```javascript
// Primitive: Pass-by-value
let x = 10;
let y = x;
y = 20;
console.log(x); // 10 (unchanged)

// Reference: Pass-by-reference
let user1 = { name: "Utkarsh" };
let user2 = user1;
user2.name = "Alex";
console.log(user1.name); // "Alex" (mutates shared heap object)
```

---

### Q3: `typeof` Results, `typeof null`, `NaN`, and `Infinity`
**Question:** What is the result of `typeof null`? What are `NaN` and `Infinity`?

**Answer:**
1. `typeof null === "object"`: Legacy bug in JS engine from 1995 (type tag `000` for objects).
2. `NaN` (Not a Number): Numeric value representing invalid arithmetic (`'abc' * 2`). `typeof NaN === "number"`. Note: `NaN === NaN` is `false`; use `Number.isNaN(val)`.
3. `Infinity`: Numeric overflow (`1 / 0`). `typeof Infinity === "number"`.

---

### Q4: Object Inspection: `Object.keys()` vs `Object.values()` vs `Object.entries()`
**Question:** Compare `Object.keys()`, `Object.values()`, and `Object.entries()`.

**Answer:**
```javascript
const user = { name: "Utkarsh", role: "Developer", age: 24 };

console.log(Object.keys(user));   // ['name', 'role', 'age']
console.log(Object.values(user)); // ['Utkarsh', 'Developer', 24]
console.log(Object.entries(user));// [['name', 'Utkarsh'], ['role', 'Developer'], ['age', 24]]

// Iterate key-value pairs cleanly:
for (const [key, val] of Object.entries(user)) {
  console.log(`${key}: ${val}`);
}
```

---

### Q5: `Object.freeze()` vs `Object.seal()`
**Question:** What is the difference between `Object.freeze()` and `Object.seal()`?

**Answer:**
| Feature | Normal Object | `Object.seal(obj)` | `Object.freeze(obj)` |
| :--- | :--- | :--- | :--- |
| **Add New Properties** | ✅ Allowed | ❌ Prevented | ❌ Prevented |
| **Delete Existing Properties** | ✅ Allowed | ❌ Prevented | ❌ Prevented |
| **Modify Existing Values** | ✅ Allowed | ✅ **Allowed** | ❌ Prevented |
| **Reconfigure Descriptors** | ✅ Allowed | ❌ Prevented | ❌ Prevented |

```javascript
const sealedObj = Object.seal({ a: 1 });
sealedObj.a = 99; // ✅ Allowed
sealedObj.b = 2;  // ❌ Fails (silently or TypeError in strict)

const frozenObj = Object.freeze({ a: 1 });
frozenObj.a = 99; // ❌ Fails
```

---

### Q6: `forEach()` vs `map()`: Why Doesn't `map()` Work the Same Way as `forEach()`?
**Question:** Compare `forEach()` and `map()`. Why shouldn't you use `map()` when you don't use the return value?

**Answer:**
- **`forEach(callback)`**:
  - Iterates over array elements and executes side effects.
  - **Returns `undefined`**.
  - Does not allocate a new array.
- **`map(callback)`**:
  - Transforms each element and **returns a brand new array** of identical length.
  - Pure transformation. Using `map` without using its returned array wastes memory allocations.

```javascript
const nums = [1, 2, 3];
// forEach for side-effects:
nums.forEach(n => console.log(n * 2));

// map for transformation:
const doubled = nums.map(n => n * 2); // [2, 4, 6]
```

---

### Q7: DOM APIs: `innerHTML` vs `innerText` vs `textContent`
**Question:** Explain the security and performance differences between `innerHTML`, `innerText`, and `textContent`.

**Answer:**
- **`innerHTML`**: Parses and renders HTML markup. Risky for XSS attacks when inserting unsanitized user inputs.
- **`innerText`**: Returns only visible text rendered on screen (respects CSS `display: none`). Forces browser layout reflow.
- **`textContent`**: Returns text content of all nodes including hidden tags. Fast and safe from XSS.

---

### Q8: What are First-Class Functions and Higher-Order Functions?
**Question:** What are First-Class Functions and Higher-Order Functions in JavaScript?

**Answer:**
- **First-Class Functions**: Functions are treated as first-class citizens (can be assigned to variables, passed as arguments, and returned from functions).
- **Higher-Order Function (HOF)**: A function that takes one or more functions as arguments OR returns a function (e.g., `map`, `filter`, `reduce`, `setTimeout`, custom decorators).
