# 📜 JavaScript - Easy Questions

> **Topics Covered:** `var` vs `let` vs `const`, Hoisting & Temporal Dead Zone (TDZ), Data Types in JS (7 Primitives + Reference Types), Stack vs Heap Memory, `typeof` & `typeof null`, `NaN` & `Infinity`, Type Coercion vs Conversion, Truthy and Falsy Values, Array Core Methods (`push`, `pop`, `shift`, `unshift`, `slice`, `splice`), Spread vs Rest Operator, Destructuring, ES6 Features Overview, Pure Functions, Arrow Functions vs Regular Functions, String Methods (`substring`, `substr`, `slice`), DOM APIs (`getElementById`, `createElement`, `innerHTML`, `innerText`, `textContent`), `e.preventDefault()`.

---

### Q1: `var` vs `let` vs `const`, Hoisting & Temporal Dead Zone (TDZ) ⭐
**Question:** What is the difference between `var`, `let`, and `const`? Explain Hoisting and TDZ.

**Answer:**
| Feature | `var` | `let` | `const` |
| :--- | :--- | :--- | :--- |
| **Scope** | Function Scope | Block Scope (`{}`) | Block Scope (`{}`) |
| **Hoisting** | Hoisted & initialized to `undefined` | Hoisted but placed in **TDZ** | Hoisted but placed in **TDZ** |
| **Re-declaration** | Allowed in same scope | Throws `SyntaxError` | Throws `SyntaxError` |
| **Re-assignment** | Allowed | Allowed | Throws `TypeError` |

**Temporal Dead Zone (TDZ):**
The phase between entering the scope and the actual variable declaration being evaluated. Accessing the variable during this time throws a `ReferenceError`.

```javascript
console.log(a); // undefined (hoisted with default undefined)
// console.log(b); // ReferenceError: Cannot access 'b' before initialization (TDZ)

var a = 10;
let b = 20; // TDZ for 'b' ends here
```

---

### Q2: Data Types in JavaScript & Primitive vs Reference Types
**Question:** What are the data types in JavaScript? Explain Primitive vs Reference types (Stack vs Heap).

**Answer:**
- **7 Primitive Data Types** (Stored directly in **Stack**, immutable value, passed by value):
  1. `string`
  2. `number`
  3. `bigint`
  4. `boolean`
  5. `undefined`
  6. `symbol`
  7. `null`
- **Reference Types** (Stored in **Heap**, variable on stack holds memory reference pointer, passed by reference):
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
console.log(obj1.name); // "Alex" (mutates shared heap object)
```

---

### Q3: `typeof null`, `NaN`, and `Infinity`
**Question:** What is the result of `typeof null`? What is `NaN` and `Infinity`?

**Answer:**
1. **`typeof null` returns `"object"`**: This is a historical bug in JavaScript from its first 1995 release where type tags stored `000` for objects and `null` was represented as a NULL pointer (`0x00`).
2. **`NaN` (Not a Number)**: A special numeric value indicating an invalid arithmetic operation (`0 / 0` or `'hello' * 2`).
   - `typeof NaN === "number"`.
   - `NaN === NaN` is `false` (use `Number.isNaN(val)` to check).
3. **`Infinity`**: Numeric value representing positive infinity (`1 / 0`).
   - `typeof Infinity === "number"`.

---

### Q4: Type Coercion (Implicit) vs Type Conversion (Explicit)
**Question:** What is type coercion vs explicit type conversion?

**Answer:**
- **Implicit Coercion**: JavaScript automatically converts types behind the scenes:
  - `+` operator with a string triggers string concatenation: `'5' + 2 = '52'`.
  - `-`, `*`, `/` operators trigger numeric conversion: `'5' - 2 = 3`, `'6' * '2' = 12`.
  - `==` performs loose equality with type coercion (`5 == '5'` is `true`), whereas `===` performs strict equality without coercion (`5 === '5'` is `false`).
- **Explicit Conversion**: Manually converting types using `Number("42")`, `String(123)`, `Boolean(1)`.

---

### Q5: Truthy and Falsy Values
**Question:** What are all the falsy values in JavaScript?

**Answer:**
There are exactly 8 falsy values in JavaScript. Everything else is truthy (including empty arrays `[]` and empty objects `{}`):
1. `false`
2. `0` (and `-0`)
3. `0n` (BigInt zero)
4. `""` (Empty string)
5. `null`
6. `undefined`
7. `NaN`
8. `document.all` (browser legacy)

---

### Q6: Can a `const` Object or Array be Modified?
**Question:** Can you modify properties of an object or elements of an array declared with `const`? How to make an object truly immutable?

**Answer:**
- **Yes**: `const` prevents re-assigning the **variable identifier** (the memory reference on the stack). It does not freeze the underlying object properties on the heap.
- To prevent mutating properties, use **`Object.freeze()`** (shallow freeze) or `Object.seal()`.

```javascript
const user = { name: "Utkarsh", age: 24 };
user.age = 25; // ✅ Allowed
// user = { name: "Other" }; // ❌ TypeError: Assignment to constant variable

Object.freeze(user);
user.age = 30; // Fails silently (or throws in strict mode)
console.log(user.age); // 25
```

---

### Q7: Array Core Methods: `push`, `pop`, `shift`, `unshift`, `splice`, `slice`
**Question:** Compare `push`, `pop`, `shift`, `unshift`, `splice`, and `slice`. Which ones mutate the array?

**Answer:**
| Method | Description | Mutates Original Array? | Returns |
| :--- | :--- | :--- | :--- |
| `push(...items)` | Adds items to the **end** | ✅ Yes | New array `length` |
| `pop()` | Removes item from the **end** | ✅ Yes | Removed item |
| `unshift(...items)` | Adds items to the **beginning** | ✅ Yes | New array `length` |
| `shift()` | Removes item from the **beginning** | ✅ Yes | Removed item |
| `splice(start, count, ...items)` | Removes/replaces/adds items at index | ✅ Yes | Array of removed items |
| `slice(start, end)` | Extracts shallow copy slice between indices | ❌ No | New array slice |

```javascript
const arr = [1, 2, 3, 4, 5];
const removed = arr.splice(1, 2, 99); // arr is now [1, 99, 4, 5], removed is [2, 3]
const sub = arr.slice(0, 2);          // arr remains [1, 99, 4, 5], sub is [1, 99]
```

---

### Q8: Spread Operator (`...`) vs Rest Operator (`...`)
**Question:** Differentiate between Spread and Rest operators with examples.

**Answer:**
- **Spread Operator**: Expands / unpacks elements of an iterable (array, object, string).
- **Rest Operator**: Condenses / gathers multiple individual values into a single array structure.

```javascript
// Rest: Function parameters & Destructuring rest
function sumAll(...numbers) {
  return numbers.reduce((acc, n) => acc + n, 0);
}
console.log(sumAll(1, 2, 3, 4)); // 10

const [first, ...remaining] = [10, 20, 30, 40];

// Spread: Array & Object cloning/merging
const nums = [1, 2];
const combined = [...nums, 3, 4]; // [1, 2, 3, 4]
const user = { name: "Utkarsh", role: "Dev" };
const updated = { ...user, role: "Lead", country: "India" };
```

---

### Q9: Array & Object Destructuring
**Question:** How does Destructuring work in JavaScript?

**Answer:**
```javascript
// Array Destructuring with default values & skip
const colors = ["red", "green", "blue"];
const [primary, , accent = "yellow"] = colors;
console.log(primary, accent); // "red", "blue"

// Object Destructuring with renaming & defaults
const profile = { username: "utkarsh", stats: { score: 98 } };
const { username: handle, stats: { score }, role = "user" } = profile;
console.log(handle, score, role); // "utkarsh", 98, "user"
```

---

### Q10: Arrow Functions vs Regular Functions
**Question:** What are the key differences between Arrow Functions and Regular Functions?

**Answer:**
1. **`this` Binding**: Arrow functions do not have their own `this`. They capture `this` lexically from their enclosing lexical context.
2. **`arguments` Object**: Arrow functions do not have an `arguments` object (use rest `...args` instead).
3. **Constructor**: Arrow functions cannot be invoked with `new` (cannot act as constructors).
4. **No `prototype`**: Arrow functions do not have a `.prototype` property.

```javascript
const obj = {
  name: "Utkarsh",
  regularFn: function() {
    console.log("Regular this:", this.name);
  },
  arrowFn: () => {
    console.log("Arrow this:", this.name); // 'this' refers to outer/global window
  }
};
obj.regularFn(); // "Regular this: Utkarsh"
obj.arrowFn();    // "Arrow this: undefined"
```

---

### Q11: Pure Functions & Side Effects
**Question:** What is a Pure Function? Give examples of pure vs impure functions.

**Answer:**
A **Pure Function** satisfies two rules:
1. **Deterministic**: Returns the exact same output every time given the same inputs.
2. **No Side Effects**: Does not mutate external variables, modify input parameters, make network calls, or write to I/O / disk.

```javascript
// Pure
const add = (a, b) => a + b;

// Impure (Mutates external state)
let counter = 0;
const increment = () => ++counter;

// Impure (Mutates input argument)
const addToArray = (arr, item) => {
  arr.push(item); // Side effect!
  return arr;
};
```

---

### Q12: DOM APIs: `innerHTML` vs `innerText` vs `textContent`
**Question:** Compare `innerHTML`, `innerText`, and `textContent`.

**Answer:**
- **`innerHTML`**: Parses and renders HTML tags. High performance cost; susceptible to **XSS (Cross-Site Scripting)** if inserting unsanitized user input.
- **`innerText`**: Returns visible text rendered on screen. Respects CSS (omits text inside `display: none` elements). Triggers layout reflow.
- **`textContent`**: Returns raw text of all nodes including hidden `<script>` and `display: none` elements. Fast and safe from XSS.

---

### Q13: `e.preventDefault()` vs `e.stopPropagation()`
**Question:** What is the difference between `e.preventDefault()` and `e.stopPropagation()`?

**Answer:**
- **`e.preventDefault()`**: Cancels the browser's default action for the event (e.g., stops a `<form>` from reloading the page, stops an `<a>` link from navigating).
- **`e.stopPropagation()`**: Stops the event from bubbling up (or capturing down) the DOM tree to parent listeners.
---

### Q14: Scope in JavaScript (Global, Function, Block Scope)
**Question:** What is scope in JavaScript? Explain Global, Function, and Block scope.

**Answer:**
Scope determines where a variable can be accessed in a program.

1. **Global Scope**: Variables declared outside any function or block are accessible anywhere in the program.
2. **Function Scope (`var`)**: Variables declared inside a function are only accessible within that function.
3. **Block Scope (`let`, `const`)**: Variables declared inside curly braces `{ ... }` cannot be accessed outside that block.

```javascript
let globalVariable = 10;

function test() {
  let functionVariable = 20;

  if (true) {
    let blockVariable = 30;
    console.log(globalVariable);   // 10
    console.log(functionVariable); // 20
    console.log(blockVariable);    // 30
  }
  // console.log(blockVariable);   // ReferenceError: blockVariable is not defined
}
test();
```

---

### Q15: Lexical Scope and Scope Chaining
**Question:** What is Lexical Scope and Scope Chaining in JavaScript?

**Answer:**
- **Lexical Scope**: The accessibility of a variable is determined by its physical location/nesting in the source code. An inner function can access variables defined in its outer enclosing scopes.
- **Scope Chaining**: The lookup mechanism JavaScript uses to resolve a variable. If a variable is not found in the current local scope, JavaScript searches the outer lexical parent scope and continues upward until it reaches the global scope.

```javascript
const a = 10;

function outer() {
  const b = 20;

  function inner() {
    const c = 30;
    console.log(a); // 10 (From Global Scope)
    console.log(b); // 20 (From Outer Scope)
    console.log(c); // 30 (From Local Scope)
  }
  inner();
}
outer();

/* Lookup Chain:
   inner scope
        ↓
   outer scope
        ↓
   global scope
*/
```

---

### Q16: What is a ReferenceError?
**Question:** What is a `ReferenceError` in JavaScript?

**Answer:**
A `ReferenceError` is thrown when code attempts to access a variable or reference that does not exist in any accessible scope, or before initialization in the TDZ.

```javascript
// 1. Variable not declared:
// console.log(x); // ReferenceError: x is not defined

// 2. Accessing let/const in Temporal Dead Zone:
// console.log(a); // ReferenceError: Cannot access 'a' before initialization
let a = 10;
```

---

### Q17: Callback Functions and Callback Hell
**Question:** What is a callback function and what is Callback Hell? How do you resolve it?

**Answer:**
- **Callback Function**: A function passed as an argument to another function, intended to be executed at a later time.
- **Callback Hell (Pyramid of Doom)**: Occurs when multiple asynchronous callbacks are deeply nested within one another, making code unreadable, brittle, and hard to debug.
- **Solution**: Refactor using ES6 **Promises** or **`async`/`await`**.

```javascript
// Basic Callback
function greet(name, callback) {
  console.log("Hello " + name);
  callback();
}
greet("Utkarsh", () => console.log("Task completed"));

// Callback Hell Example:
getUser((user) => {
  getOrders(user, (orders) => {
    getPayment(orders, (payment) => {
      getDetails(payment, (details) => {
        console.log(details);
      });
    });
  });
});

// Modern Async/Await Refactor:
async function showDetails() {
  try {
    const user = await getUser();
    const orders = await getOrders(user);
    const payment = await getPayment(orders);
    const details = await getDetails(payment);
    console.log(details);
  } catch (err) {
    console.error("Error:", err);
  }
}
```
