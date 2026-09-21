# 📜 JavaScript - Medium Questions

> **Topics Covered:** Closures (Deep Dive), Higher Order Array Methods (`map`, `filter`, `reduce`, `find`, `some`, `every`, `flat`), `this` Keyword & `call` / `apply` / `bind`, Shallow Copy vs Deep Copy (`structuredClone`, JSON parse, lodash), Promises & Async/Await, Promise Combinators (`Promise.all`, `allSettled`, `race`, `any`), Debouncing vs Throttling (Deep Dive), Event Bubbling, Capturing & Event Delegation, Lexical Scoping & Scope Chain, Currying.

---

### Q1: Closures in JavaScript ⭐⭐⭐
**Question:** What is a Closure in JavaScript? How does it work under the hood? Provide practical use cases and an interview output question.

**Answer:**
A **Closure** is the combination of a function bundled together with references to its surrounding lexical environment. In simple terms: **An inner function has access to the variables of its outer function even after the outer function has closed / returned.**

#### How it works:
When a function is defined, it retains a hidden reference `[[Environment]]` pointing to the Lexical Environment in which it was created.

```javascript
function createCounter() {
  let count = 0; // Private variable encapsulated in closure
  return {
    increment: () => ++count,
    decrement: () => --count,
    getCount: () => count
  };
}

const counter = createCounter();
console.log(counter.increment()); // 1
console.log(counter.increment()); // 2
console.log(counter.getCount());  // 2
// count variable cannot be accessed or modified directly from the outside!
```

#### Common Use Cases:
1. **Data Encapsulation / Private State**: Emulating private variables.
2. **Function Currying & Partial Application**.
3. **Memoization / Caching**.
4. **Event Handlers & Callback Timers**.

#### Classic Interview Loop Puzzle:
```javascript
// Problem:
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
// Output: 3, 3, 3 (because 'var' is function-scoped; by the time callback runs, i is 3)

// Solution 1 (ES6 Block Scope with let):
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
// Output: 0, 1, 2 (each iteration gets a new lexical binding of i)

// Solution 2 (Closure with IIFE):
for (var i = 0; i < 3; i++) {
  ((j) => setTimeout(() => console.log(j), 100))(i);
}
// Output: 0, 1, 2
```

---

### Q2: Promises & Async/Await Deep Dive ⭐⭐⭐
**Question:** What is a Promise? Explain Promise states, chaining, and error handling with `async/await`.

**Answer:**
A **Promise** is an object representing the eventual completion (or failure) of an asynchronous operation and its resulting value.

#### 3 Promise States:
1. **`pending`**: Initial state, neither fulfilled nor rejected.
2. **`fulfilled`**: Operation completed successfully (`resolve(value)`).
3. **`rejected`**: Operation failed (`reject(error)`).

```javascript
// Creating a Promise
function fetchUserData(userId) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (userId > 0) {
        resolve({ id: userId, name: "Utkarsh Singh" });
      } else {
        reject(new Error("Invalid User ID"));
      }
    }, 500);
  });
}

// Consuming with async/await & try/catch
async function getUser() {
  try {
    const user = await fetchUserData(1);
    console.log("User Loaded:", user.name);
  } catch (err) {
    console.error("Fetch Error:", err.message);
  } finally {
    console.log("Operation Complete");
  }
}
getUser();
```

---

### Q3: Promise Combinators: `Promise.all`, `allSettled`, `race`, `any`
**Question:** Compare `Promise.all()`, `Promise.allSettled()`, `Promise.race()`, and `Promise.any()`.

**Answer:**
| Method | Description | Resolves When | Rejects When |
| :--- | :--- | :--- | :--- |
| **`Promise.all`** | Runs promises in parallel | **ALL** promises resolve | **ANY single** promise rejects (Fail-fast) |
| **`Promise.allSettled`** | Runs promises in parallel | **ALL** promises settle (resolve or reject) | Never rejects. Returns array of `{status, value/reason}` |
| **`Promise.race`** | Returns the first settled promise | **FIRST** promise settles (resolves or rejects) | **FIRST** promise rejects |
| **`Promise.any`** | Returns the first fulfilled promise | **FIRST** promise resolves | **ALL** promises reject (`AggregateError`) |

```javascript
const p1 = Promise.resolve("A");
const p2 = Promise.reject("B Error");
const p3 = Promise.resolve("C");

Promise.allSettled([p1, p2, p3]).then(results => console.log(results));
/* [
  { status: 'fulfilled', value: 'A' },
  { status: 'rejected', reason: 'B Error' },
  { status: 'fulfilled', value: 'C' }
] */
```

---

### Q4: Debouncing vs Throttling Deep Dive ⚡ ⭐⭐⭐
**Question:** Explain Debouncing vs Throttling with real-world examples, implementation functions, and use cases.

**Answer:**
- **Debouncing**: Delays execution of a function until after a specific duration of **inactivity (silence)** has passed since the last trigger.
  - *Real-life analogy*: An elevator waits for 5 seconds after the last person walks in before closing doors.
  - *Best for*: Search bar auto-complete, auto-saving drafts, window resizing.
- **Throttling**: Ensures a function is executed at most **once every specified time interval**, regardless of how many times the event fires.
  - *Real-life analogy*: A machine gun firing bullets with a fixed cooldown rate no matter how fast you pull the trigger.
  - *Best for*: Infinite scroll loading, window scroll progress bars, mouse move tracking, game shoot buttons.

#### Implementation:
```javascript
// Debounce Function
function debounce(fn, delay) {
  let timerId;
  return function(...args) {
    clearTimeout(timerId);
    timerId = setTimeout(() => {
      fn.apply(this, args);
    }, delay);
  };
}

// Throttle Function
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

// Usage
const handleSearch = debounce((query) => console.log("Searching for:", query), 300);
const handleScroll = throttle(() => console.log("Scroll event fired"), 200);
```

---

### Q5: Explicit Binding: `call` vs `apply` vs `bind`
**Question:** Differentiate between `call()`, `apply()`, and `bind()`.

**Answer:**
All three methods are used to set the `this` context of a function explicitly:
1. **`call(thisArg, arg1, arg2, ...)`**: Invokes the function immediately with comma-separated arguments.
2. **`apply(thisArg, [argsArray])`**: Invokes the function immediately with arguments passed as an array.
3. **`bind(thisArg, arg1, arg2, ...)`**: Does **not** invoke immediately; returns a **new copy of the function** bound permanently to the provided `this` context.

```javascript
const person = { name: "Utkarsh" };

function greet(greeting, punctuation) {
  console.log(`${greeting}, ${this.name}${punctuation}`);
}

greet.call(person, "Hello", "!");        // "Hello, Utkarsh!"
greet.apply(person, ["Welcome", "."]);    // "Welcome, Utkarsh."

const boundGreet = greet.bind(person, "Hi");
boundGreet("!!");                         // "Hi, Utkarsh!!"
```

---

### Q6: Shallow Copy vs Deep Copy
**Question:** What is the difference between Shallow Copy and Deep Copy? What are all the ways to create them?

**Answer:**
- **Shallow Copy**: Copies the top-level properties. If a property is a reference to a nested object/array, both copies share the same nested reference.
  - *Methods:* Spread operator `{ ...obj }`, `Object.assign({}, obj)`, `[...arr]`, `arr.slice()`.
- **Deep Copy**: Clones all levels recursively. Nested objects are duplicated into completely independent memory allocations in the heap.
  - *Methods:*
    1. **`structuredClone(obj)`** (Modern Native Standard - handles Maps, Sets, Dates, circular refs).
    2. **`JSON.parse(JSON.stringify(obj))`** (Quick, but drops `undefined`, functions, symbols, and fails on circular references).
    3. **Lodash `_.cloneDeep(obj)`**.

```javascript
const original = { name: "Utkarsh", address: { city: "Delhi" } };

// Shallow Copy
const shallow = { ...original };
shallow.address.city = "Mumbai";
console.log(original.address.city); // "Mumbai" (Mutated original nested object!)

// Deep Copy
const deep = structuredClone(original);
deep.address.city = "Bangalore";
console.log(original.address.city); // "Mumbai" (Original protected)
```

---

### Q7: Higher-Order Array Methods: `map`, `filter`, `reduce`
**Question:** How do `map`, `filter`, and `reduce` work? Write a `reduce` example to group items by property.

**Answer:**
```javascript
const items = [
  { id: 1, category: "Electronics", price: 300 },
  { id: 2, category: "Clothing", price: 50 },
  { id: 3, category: "Electronics", price: 700 }
];

// 1. map: Transforms each element into a new array
const names = items.map(item => item.category);

// 2. filter: Filters elements based on predicate condition
const expensive = items.filter(item => item.price > 100);

// 3. reduce: Groups items by category
const grouped = items.reduce((acc, item) => {
  acc[item.category] = acc[item.category] || [];
  acc[item.category].push(item);
  return acc;
}, {});
console.log(grouped);
```

---

### Q8: Event Bubbling, Capturing, and Event Delegation
**Question:** Explain Event Propagation (Bubbling vs Capturing) and Event Delegation.

**Answer:**
1. **Event Flow Phases:**
   - **Capturing Phase (Trickling)**: Event travels down from `window` $ightarrow$ `document` $ightarrow$ `<html>` $ightarrow$ target element.
   - **Target Phase**: Event arrives at the actual element clicked.
   - **Bubbling Phase**: Event bubbles back up from the target $ightarrow$ parent elements $ightarrow$ `window` (default phase for `addEventListener`).
2. **Event Delegation**:
   Instead of attaching event listeners to hundreds of individual child items (`<li>`), attach a single listener to the parent container (`<ul>`) and use `e.target` to identify which child was clicked.
   - *Benefits:* Massive memory savings; automatically handles dynamically added child elements.

```javascript
document.getElementById("todo-list").addEventListener("click", (e) => {
  if (e.target && e.target.nodeName === "BUTTON") {
    console.log("Delete button clicked for task ID:", e.target.dataset.id);
  }
});
```

---

### Q9: Function Currying
**Question:** What is Function Currying? Implement a curried sum function `sum(1)(2)(3)()`.

**Answer:**
- **Currying** is a functional programming technique where a function with multiple arguments is transformed into a sequence of nesting functions, each taking a single argument.

```javascript
// Infinite Currying with empty termination
function sum(a) {
  return function(b) {
    if (b !== undefined) {
      return sum(a + b);
    }
    return a;
  };
}

console.log(sum(1)(2)(3)(4)()); // 10
```
