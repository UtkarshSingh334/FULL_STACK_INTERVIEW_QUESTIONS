# 📜 JavaScript - Medium & Applied Concepts

> **Topics Covered:** Promises (States, Creation, Chaining, Error Handling, Nesting, Promise vs Callback vs Async/Await), Promise Static Methods (`Promise.all`, `allSettled`, `race`, `any`, `resolve`, `reject` + Comparison Matrix), Async/Await (Execution, Try/Catch, Sequential vs Parallel), Scope Chain & Lexical vs Dynamic Scope, Closures Deep Dive, Callbacks & Callback Hell, Event Propagation (Capturing, Target, Bubbling), Event Bubbling & `stopPropagation()`, Event Capturing, Event Delegation, `this` Binding & Function Borrowing (`call`, `apply`, `bind`), Function Currying & Partial Application, Higher-Order Functions, Array `reduce()` Deep Dive & Comparison Table, Shallow Copy vs Deep Copy.

---

## 1. What is a Promise and What are its 3 States?

### Answer
A **Promise** is an object representing the eventual completion or failure of an asynchronous operation.
- **3 States:**
  1. **Pending**: Initial state, operation is ongoing.
  2. **Fulfilled (Resolved)**: Operation completed successfully (`resolve(value)`).
  3. **Rejected**: Operation failed (`reject(error)`).

### Example
```js
const promise = new Promise((resolve, reject) => {
    const success = true;
    if (success) resolve("Operation Successful");
    else reject("Operation Failed");
});

promise
    .then(data => console.log(data))
    .catch(err => console.error(err));
```

### Output
```
Operation Successful
```

---

## 2. Promise Chaining & Error Handling (.then, .catch, .finally)

### Answer
- **Promise Chaining**: Returning a value or another Promise from a `.then()` handler to execute asynchronous tasks in sequence.
- **`.catch()`**: Catches errors from any step in the preceding chain.
- **`.finally()`**: Executes cleanup logic after settlement regardless of success or failure.

### Example
```js
function calculate(num) {
    return Promise.resolve(num)
        .then(n => n * 2)
        .then(n => n + 5)
        .then(n => console.log("Final Result:", n))
        .catch(err => console.error("Error in chain:", err))
        .finally(() => console.log("Chain complete."));
}

calculate(10);
```

### Output
```
Final Result: 25
Chain complete.
```

---

## 3. Promise Static Methods: all, allSettled, race, any, resolve, reject

### Answer
| Method | Resolves When | Rejects When | Return Value on Success |
| :--- | :--- | :--- | :--- |
| **`Promise.all`** | **ALL** promises resolve | **ANY** promise rejects (Fail-Fast) | Array of all resolved values `[v1, v2]` |
| **`Promise.allSettled`**| **ALL** promises settle | Never rejects | Array of status objects `[{status, value/reason}]` |
| **`Promise.race`** | **FIRST** promise settles (resolve/reject) | **FIRST** promise rejects | Value/Reason of the fastest settled promise |
| **`Promise.any`** | **FIRST** promise **fulfills** | **ALL** promises reject | Value of the fastest fulfilled promise (or `AggregateError`) |

### Example
```js
const p1 = Promise.resolve("A");
const p2 = Promise.reject("B Failed");
const p3 = Promise.resolve("C");

// Promise.allSettled waits for all regardless of errors:
Promise.allSettled([p1, p2, p3])
    .then(results => console.log(results));
```

### Output
```js
[
  { status: 'fulfilled', value: 'A' },
  { status: 'rejected', reason: 'B Failed' },
  { status: 'fulfilled', value: 'C' }
]
```

---

## 4. Async / Await: How It Works & Error Handling (try/catch)

### Answer
- **`async`**: Declares an asynchronous function. Always returns a Promise.
- **`await`**: Pauses function execution until the awaited Promise settles.
- **Error Handling**: Wrapped in synchronous-looking `try...catch` blocks.

### Example
```js
async function fetchUserData(userId) {
    try {
        if (!userId) throw new Error("User ID is required");
        const response = await fetch(`https://jsonplaceholder.typicode.com/users/${userId}`);
        const user = await response.json();
        return user.name;
    } catch (error) {
        console.error("Caught in try/catch:", error.message);
    } finally {
        console.log("Fetch attempt finished.");
    }
}

fetchUserData(1).then(name => console.log("User:", name));
```

---

## 5. Sequential vs Parallel Execution with async/await

### Answer
- **Sequential**: Awaiting promises one by one in sequence (Takes $T_1 + T_2$).
- **Parallel**: Firing all promises simultaneously and awaiting `Promise.all()` (Takes $\max(T_1, T_2)$).

### Example
```js
const delay = (ms, val) => new Promise(res => setTimeout(() => res(val), ms));

// Parallel Execution (Fast: max(100ms, 100ms) = 100ms)
async function parallelRun() {
    console.time("Parallel");
    const [res1, res2] = await Promise.all([delay(100, "1"), delay(100, "2")]);
    console.timeEnd("Parallel");
    console.log("Results:", res1, res2);
}
parallelRun();
```

---

## 6. What is the Scope Chain and How Does JavaScript Find a Variable?

### Answer
The **Scope Chain** is the hierarchical lookup process JavaScript uses to resolve variable references:
1. Searches the **Current Local Scope**.
2. If not found, searches the **Outer Lexical Parent Scope**.
3. Continues climbing upward until it reaches the **Global Scope**.
4. If not found in the global scope, throws a **`ReferenceError`**.

```
Current Local Scope
        ↓
Outer Lexical Scope
        ↓
   Global Scope
```

### Example
```js
const globalName = "Utkarsh";

function outer() {
    const outerRole = "Developer";
    function inner() {
        const innerSkill = "JavaScript";
        console.log(innerSkill); // Local
        console.log(outerRole);  // Outer
        console.log(globalName); // Global
    }
    inner();
}
outer();
```

---

## 7. What is a Closure in JavaScript?

### Answer
A **Closure** is created when an inner function remembers and retains access to its outer function's lexical variables even after the outer function has finished executing and returned.

### Example
```js
function createCounter() {
    let count = 0; // Private encapsulated state
    return function() {
        return ++count;
    };
}

const counter = createCounter();
console.log(counter()); // 1
console.log(counter()); // 2
console.log(counter()); // 3
```

---

## 8. What is Callback Hell and How Can It Be Avoided?

### Answer
**Callback Hell** occurs when multiple asynchronous callbacks are nested deeply, creating unreadable and fragile pyramid code. It is avoided using **Promises** or **`async/await`**.

### Example
```js
// ❌ Callback Hell
getUser(id, (user) => {
    getOrders(user.id, (orders) => {
        getPayment(orders[0].id, (payment) => {
            console.log(payment);
        });
    });
});

// ✅ Refactored with async/await
async function getPaymentFlow(id) {
    const user = await getUser(id);
    const orders = await getOrders(user.id);
    const payment = await getPayment(orders[0].id);
    console.log(payment);
}
```

---

## 9. Event Propagation: Capturing, Target, and Bubbling Phases

### Answer
When an event occurs on a DOM element, it passes through 3 phases:
1. **Capturing Phase**: Event descends from `window` $ightarrow$ `document` $ightarrow$ ancestors down to target.
2. **Target Phase**: Event arrives at the target element clicked.
3. **Bubbling Phase**: Event bubbles upward from target back through ancestors up to `window`.

```
Capturing Phase (Downward)  -->  Target Phase  -->  Bubbling Phase (Upward)
```

---

## 10. Event Bubbling & How to Stop It with stopPropagation()

### Answer
**Event Bubbling** is the default phase where event handlers fire on the target and bubble upward to all parent ancestors. `event.stopPropagation()` halts this upward propagation.

### Example
```js
document.getElementById("parent").addEventListener("click", () => {
    console.log("Parent clicked");
});

document.getElementById("child").addEventListener("click", (event) => {
    console.log("Child clicked");
    event.stopPropagation(); // Prevents "Parent clicked" from firing!
});
```

---

## 11. Event Capturing: How to Enable It

### Answer
**Event Capturing** handlers execute during the downward journey before reaching the target. Pass `{ capture: true }` or `true` as the third parameter to `addEventListener`.

### Example
```js
parent.addEventListener("click", () => {
    console.log("Parent (Capturing)");
}, true); // true enables Capturing
```

---

## 12. What is Event Delegation and Why is It Useful?

### Answer
**Event Delegation** is attaching a single event listener to a parent container instead of attaching listeners to multiple child elements, using `event.target` to detect which child was clicked.
- **Benefits**: Memory savings and automatic support for dynamically added child elements.

### Example
```js
document.getElementById("list").addEventListener("click", (event) => {
    if (event.target && event.target.tagName === "LI") {
        console.log("Item Clicked:", event.target.textContent);
    }
});
```

---

## 13. this Keyword, Function Borrowing & call() vs apply() vs bind()

### Answer
- **`call(thisArg, arg1, arg2)`**: Invokes function immediately with comma-separated arguments.
- **`apply(thisArg, [args])`**: Invokes function immediately with arguments array.
- **`bind(thisArg, arg1)`**: Returns a **new copy of the function** bound permanently to `thisArg`.

### Example
```js
const user = { name: "Utkarsh" };

function greet(greeting, punctuation) {
    console.log(`${greeting}, I am ${this.name}${punctuation}`);
}

greet.call(user, "Hello", "!");        // "Hello, I am Utkarsh!"
greet.apply(user, ["Hi", "."]);        // "Hi, I am Utkarsh."
const bound = greet.bind(user, "Hey");
bound("!!");                           // "Hey, I am Utkarsh!!"
```

---

## 14. What is Function Currying?

### Answer
**Currying** transforms a function with multiple arguments into a sequence of nested functions, each taking a single argument ($f(a, b, c) ightarrow f(a)(b)(c)$).

### Example
```js
// Standard Currying:
function add(a) {
    return function(b) {
        return function(c) {
            return a + b + c;
        };
    };
}
console.log(add(1)(2)(3)); // 6

// Arrow Currying:
const addCurry = a => b => c => a + b + c;
console.log(addCurry(10)(20)(30)); // 60
```

---

## 15. Array.prototype.reduce() Deep Dive

### Answer
`reduce(callback, initialValue)` executes a reducer function across each element, returning a single accumulated value.
- **Parameters**: `accumulator (acc)`, `currentValue (curr)`, `index`, `array`.

### Example
```js
// 1. Sum
const nums = [1, 2, 3, 4];
const sum = nums.reduce((acc, curr) => acc + curr, 0); // 10

// 2. Group Objects by Property
const items = [{ cat: "Fruit", name: "Apple" }, { cat: "Veg", name: "Carrot" }, { cat: "Fruit", name: "Banana" }];
const grouped = items.reduce((acc, item) => {
    acc[item.cat] = acc[item.cat] || [];
    acc[item.cat].push(item.name);
    return acc;
}, {});
console.log(grouped); // { Fruit: ['Apple', 'Banana'], Veg: ['Carrot'] }
```

---

## 16. Shallow Copy vs Deep Copy

### Answer
- **Shallow Copy**: Duplicates top-level properties; nested objects share the same memory pointer (`{ ...obj }`, `Object.assign()`).
- **Deep Copy**: Clones all nested levels recursively into independent memory allocations (`structuredClone(obj)`, `JSON.parse(JSON.stringify(obj))`).

### Example
```js
const original = { name: "Utkarsh", address: { city: "Delhi" } };

// Shallow Copy:
const shallow = { ...original };
shallow.address.city = "Mumbai";
console.log(original.address.city); // "Mumbai" (Original mutated!)

// Deep Copy:
const deep = structuredClone(original);
deep.address.city = "Bangalore";
console.log(original.address.city); // "Mumbai" (Original protected)
```
