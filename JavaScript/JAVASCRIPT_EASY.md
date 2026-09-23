# 📜 JavaScript - Easy & Fundamentals

> **Topics Covered:** `var` vs `let` vs `const`, Hoisting, Temporal Dead Zone (TDZ), Data Types (7 Primitives vs Reference, Stack vs Heap), `typeof` & `typeof null`, `NaN` & `Infinity`, Type Coercion vs Conversion, `==` vs `===`, `null` vs `undefined`, Truthy and Falsy, Scope (Global, Function, Block), `Object.freeze()` vs `Object.seal()`, `Object.keys()`/`values()`/`entries()`, Array Methods (`push`, `pop`, `shift`, `unshift`, `slice`, `splice`), `map()` vs `forEach()`, `filter()` vs `find()`, `some()` vs `every()`, Function Declaration vs Expression, Arrow Functions, Pure Functions, DOM Selectors & Manipulation, `innerHTML` vs `innerText` vs `textContent`, `preventDefault()`, Spread & Rest Operators, Destructuring, ES6 Core Features, Errors (`ReferenceError`, `TypeError`, `SyntaxError`), Timers (`setTimeout`, `setInterval`).

---

## 1. What is the difference between var, let, and const?

### Answer
`var`, `let`, and `const` are keywords used to declare variables in JavaScript. They differ in scope, hoisting behavior, re-declaration, and re-assignment.

| Feature | `var` | `let` | `const` |
| :--- | :--- | :--- | :--- |
| **Scope** | Function Scope | Block Scope (`{}`) | Block Scope (`{}`) |
| **Hoisting** | Hoisted and initialized to `undefined` | Hoisted but placed in TDZ | Hoisted but placed in TDZ |
| **Re-declaration** | Allowed in same scope | Throws `SyntaxError` | Throws `SyntaxError` |
| **Re-assignment** | Allowed | Allowed | Throws `TypeError` |
| **Initialization** | Optional | Optional | Mandatory upon declaration |

### Example
```js
var a = 10;
var a = 20; // Re-declaration allowed

let b = 30;
b = 40;     // Re-assignment allowed

const c = 50;
// c = 60;  // TypeError: Assignment to constant variable
```

---

## 2. What is Hoisting in JavaScript?

### Answer
**Hoisting** is JavaScript's default behavior of moving declarations to the top of their containing scope during the creation phase of the Execution Context before code is executed.
- `var` declarations are hoisted and initialized with `undefined`.
- `let` and `const` declarations are hoisted into the **Temporal Dead Zone (TDZ)** without initialization.
- Function declarations are hoisted completely with their function definitions.

### Example
```js
console.log(greeting); // undefined (var hoisted)
var greeting = "Hello!";

sayHello(); // "Hello from hoisted function!"
function sayHello() {
    console.log("Hello from hoisted function!");
}
```

### Output
```
undefined
Hello from hoisted function!
```

---

## 3. What is the Temporal Dead Zone (TDZ)?

### Answer
The **Temporal Dead Zone (TDZ)** is the period between entering a scope and the variable declaration being evaluated. Accessing a `let` or `const` variable while it is in the TDZ throws a **`ReferenceError`**.

### Example
```js
{
    // TDZ for variable 'score' starts here
    // console.log(score); // ReferenceError: Cannot access 'score' before initialization
    let score = 100; // TDZ ends here
    console.log(score); // 100
}
```

---

## 4. What are Primitive vs Reference Data Types in JavaScript?

### Answer
- **7 Primitive Data Types** (Stored directly in the **Call Stack**, immutable, compared and copied by value):
  `string`, `number`, `bigint`, `boolean`, `undefined`, `symbol`, `null`.
- **Reference Types** (Stored in the **Memory Heap**, stack variable holds a pointer reference, copied by reference):
  `Object`, `Array`, `Function`, `Date`, `Map`, `Set`.

### Example
```js
// Primitive: Pass-by-value
let x = 10;
let y = x;
y = 20;
console.log(x); // 10 (unchanged)

// Reference: Pass-by-reference
let user1 = { name: "Utkarsh" };
let user2 = user1;
user2.name = "Alex";
console.log(user1.name); // "Alex" (mutates shared object in heap)
```

---

## 5. What is the result of typeof null? What are NaN and Infinity?

### Answer
1. **`typeof null` returns `"object"`**: A historical bug in JavaScript from its first 1995 release where values had a type tag (tag `000` represented objects and `null` was represented as a NULL pointer).
2. **`NaN` (Not a Number)**: A special numeric value indicating an invalid arithmetic calculation (`"hello" * 2`).
   - `typeof NaN === "number"`
   - `NaN === NaN` evaluates to `false`. Use `Number.isNaN(val)` to check.
3. **`Infinity`**: Represents mathematical infinity (`1 / 0`). `typeof Infinity === "number"`.

### Example
```js
console.log(typeof null);      // "object"
console.log(typeof NaN);       // "number"
console.log(Number.isNaN(NaN));// true
console.log(1 / 0);            // Infinity
```

---

## 6. What is Type Coercion? Difference between == and ===

### Answer
- **Type Coercion**: The automatic or implicit conversion of values from one data type to another by JavaScript.
  - Plus operator with string concatenates: `'5' + 2 = '52'`.
  - Minus operator converts to numbers: `'5' - 2 = 3`.
- **`==` (Loose Equality)**: Compares values after performing automatic type coercion.
- **`===` (Strict Equality)**: Compares both **value and data type** without coercion.

### Example
```js
console.log(5 == "5");   // true (string "5" coerced to number 5)
console.log(5 === "5");  // false (number !== string)
console.log(null == undefined);  // true
console.log(null === undefined); // false
```

---

## 7. What are Truthy and Falsy Values?

### Answer
In JavaScript, a value is **falsy** if it evaluates to `false` in a boolean context. There are exactly 8 falsy values:
1. `false`
2. `0` and `-0`
3. `0n` (BigInt zero)
4. `""` (Empty string)
5. `null`
6. `undefined`
7. `NaN`
8. `document.all`

All other values are **truthy** (including empty arrays `[]`, empty objects `{}`, and `"0"`).

---

## 8. What is Scope? Global, Function, and Block Scope

### Answer
**Scope** determines the accessibility/visibility of variables and functions in various parts of code.
1. **Global Scope**: Variables declared outside any function or block are accessible throughout the entire program.
2. **Function Scope (`var`)**: Variables declared inside a function are accessible only within that function.
3. **Block Scope (`let`, `const`)**: Variables declared inside `{ ... }` are accessible only inside that block.

### Example
```js
let globalVar = "Global";

function testScope() {
    var funcVar = "Function";
    if (true) {
        let blockVar = "Block";
        var leaked = "Leaked from block";
        console.log(blockVar); // "Block"
    }
    console.log(leaked); // "Leaked from block"
    // console.log(blockVar); // ReferenceError: blockVar is not defined
}
testScope();
```

---

## 9. Difference between Object.freeze() and Object.seal()

### Answer
| Feature | `Object.seal(obj)` | `Object.freeze(obj)` |
| :--- | :--- | :--- |
| **Add New Properties** | ❌ Prevented | ❌ Prevented |
| **Delete Properties** | ❌ Prevented | ❌ Prevented |
| **Modify Existing Values** | ✅ **Allowed** | ❌ Prevented |

### Example
```js
const sealed = Object.seal({ a: 1 });
sealed.a = 99; // ✅ Allowed
sealed.b = 2;  // ❌ Fails

const frozen = Object.freeze({ a: 1 });
frozen.a = 99; // ❌ Fails
```

---

## 10. Difference between Object.keys(), Object.values(), and Object.entries()

### Answer
```js
const user = { name: "Utkarsh", role: "Dev", age: 24 };

console.log(Object.keys(user));   // ['name', 'role', 'age']
console.log(Object.values(user)); // ['Utkarsh', 'Dev', 24]
console.log(Object.entries(user));// [['name', 'Utkarsh'], ['role', 'Dev'], ['age', 24]]
```

---

## 11. map() vs forEach(): Why Doesn't map() Work the Same Way as forEach()?

### Answer
- **`forEach(callback)`**: Iterates over array elements and executes a callback function for side-effects. **Returns `undefined`**.
- **`map(callback)`**: Transforms each element and **returns a brand new array** of identical length containing the returned values.

### Example
```js
const nums = [1, 2, 3];

// forEach (returns undefined)
const forEachRes = nums.forEach(n => n * 2);
console.log(forEachRes); // undefined

// map (returns new transformed array)
const mapRes = nums.map(n => n * 2);
console.log(mapRes); // [2, 4, 6]
```

---

## 12. filter() vs find() and some() vs every()

### Answer
- **`filter(predicate)`**: Returns a **new array containing ALL matching items** (or empty array).
- **`find(predicate)`**: Returns the **FIRST matching element** directly (or `undefined`).
- **`some(predicate)`**: Returns `true` if **at least one element** satisfies condition.
- **`every(predicate)`**: Returns `true` only if **all elements** satisfy condition.

### Example
```js
const users = [{ id: 1, age: 17 }, { id: 2, age: 21 }, { id: 3, age: 25 }];

console.log(users.filter(u => u.age >= 18)); // [{ id: 2, age: 21 }, { id: 3, age: 25 }]
console.log(users.find(u => u.age >= 18));   // { id: 2, age: 21 }
console.log(users.some(u => u.age >= 18));   // true
console.log(users.every(u => u.age >= 18));  // false
```

---

## 13. Function Declaration vs Function Expression vs Arrow Function

### Answer
- **Function Declaration**: Hoisted completely to the top of scope; can be called before definition.
- **Function Expression**: Function assigned to a variable; variable is hoisted as `undefined`.
- **Arrow Function**: Concise syntax, does not have its own `this`, `arguments`, or `prototype`, and cannot be called with `new`.

### Example
```js
// 1. Declaration (Hoisted)
declaredFn(); // Works!
function declaredFn() { console.log("Declaration"); }

// 2. Expression
// exprFn(); // TypeError: exprFn is not a function
var exprFn = function() { console.log("Expression"); };

// 3. Arrow Function
const arrowFn = (a, b) => a + b;
```

---

## 14. What is a Pure Function?

### Answer
A **Pure Function** is a function that:
1. **Deterministic**: Given the same arguments, always returns the exact same result.
2. **No Side Effects**: Does not mutate external variables, modify input parameters, or perform I/O.

### Example
```js
// ✅ Pure Function
function add(a, b) {
    return a + b;
}

// ❌ Impure Function (Mutates external variable)
let count = 0;
function increment() {
    return ++count;
}
```

---

## 15. DOM Selectors & Difference between getElementById, querySelector, querySelectorAll

### Answer
- **`getElementById('id')`**: Selects single element by ID attribute.
- **`getElementsByClassName('class')`**: Returns a **live `HTMLCollection`** of matching elements.
- **`querySelector('cssSelector')`**: Returns the **first element** matching any valid CSS selector.
- **`querySelectorAll('cssSelector')`**: Returns a **static `NodeList`** of all matching elements (supports `.forEach()`).

### Example
```js
const header = document.getElementById("header");
const cards = document.getElementsByClassName("card"); // HTMLCollection (Live)
const firstBtn = document.querySelector(".btn.primary");
const allBtns = document.querySelectorAll("button");   // NodeList (Static)

allBtns.forEach(btn => console.log(btn.textContent));
```

---

## 16. Difference between innerHTML, innerText, and textContent

### Answer
- **`innerHTML`**: Gets or sets raw HTML markup. Vulnerable to **XSS** if used with unsanitized user inputs.
- **`innerText`**: Returns visible rendered text only (respects CSS styling like `display: none`). Triggers reflow.
- **`textContent`**: Returns raw text of all nodes including hidden tags. Fast and safe from XSS.

---

## 17. What is preventDefault() and why is it used?

### Answer
**`event.preventDefault()`** cancels the browser's default action for an event (e.g. stops `<form>` submission from reloading the page, stops `<a>` links from navigating, prevents checkbox toggling).

### Example
```js
document.querySelector("form").addEventListener("submit", (event) => {
    event.preventDefault(); // Prevents page reload
    console.log("Form data submitted via AJAX");
});
```

---

## 18. Spread Operator vs Rest Parameter

### Answer
Both use the three dots `...` syntax, but their roles are opposites:
- **Spread (`...`) $ightarrow$ EXPANDS** values from an iterable.
- **Rest (`...`) $ightarrow$ COLLECTS** multiple values into an array.

| Feature | Spread Operator | Rest Parameter |
| :--- | :--- | :--- |
| **Action** | Unpacks / expands elements | Gathers / packs elements |
| **Usage** | Function calls, Array literals, Object literals | Function parameter lists, Destructuring |
| **Example** | `const merged = [...arr1, ...arr2];` | `function sum(...nums) {}` |

### Example
```js
// Spread: Expands array/object
const arr1 = [1, 2];
const arr2 = [...arr1, 3, 4]; // [1, 2, 3, 4]

// Rest: Collects parameters into an array
function sum(...numbers) {
    return numbers.reduce((total, n) => total + n, 0);
}
console.log(sum(10, 20, 30)); // 60
```

---

## 19. Destructuring (Array & Object)

### Answer
**Destructuring** is an ES6 syntax that allows you to extract values from arrays or properties from objects into distinct variables.

### Example
```js
// Array Destructuring with default & skip
const [first, , third = 30] = [10, 20];
console.log(first, third); // 10, 30

// Object Destructuring with renaming & default
const user = { username: "utkarsh", role: "admin" };
const { username: name, role, country = "India" } = user;
console.log(name, role, country); // "utkarsh", "admin", "India"
```

---

## 20. What is a ReferenceError vs TypeError vs SyntaxError?

### Answer
- **`ReferenceError`**: Thrown when accessing a variable that does not exist in scope or before initialization in TDZ.
- **`TypeError`**: Thrown when an operation is performed on an incompatible data type (e.g. modifying `const`, calling a non-function).
- **`SyntaxError`**: Thrown when code violates JavaScript language grammar.

### Example
```js
// 1. ReferenceError
// console.log(unknownVar); // ReferenceError: unknownVar is not defined

// 2. TypeError
const num = 10;
// num = 20; // TypeError: Assignment to constant variable
// null.toString(); // TypeError: Cannot read properties of null

// 3. SyntaxError
// let a = 1; let a = 2; // SyntaxError: Identifier 'a' has already been declared
```

---

## 21. What are the Most Important ES6 Features?

### Answer
1. **`let` & `const`** (Block-scoped variables)
2. **Arrow Functions** (`() => {}`)
3. **Template Literals** (`` `Hello ${name}` ``)
4. **Destructuring** (Array & Object)
5. **Spread & Rest Operators** (`...`)
6. **Default Parameters** (`fn(x = 10)`)
7. **Classes & Modules** (`class`, `import`/`export`)
8. **Promises** (`new Promise()`)
9. **`Map`, `Set`, `Symbol`**
10. **`for...of` Loop**
