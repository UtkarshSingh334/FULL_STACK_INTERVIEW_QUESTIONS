# 📜 JavaScript - Coding Challenges & Polyfills

> **Must-Know Machine Coding Questions:** Custom Polyfill for `map()`, `filter()`, `reduce()`, Debounce with immediate flag, Throttle with leading/trailing, Deep Clone with circular reference handling, Memoization function, Custom Promise Implementation, Flatten Array, Frequency Counter, `once()` Function, Currying implementation.

---

### Q1: Custom Polyfill for `Array.prototype.map()`
```javascript
Array.prototype.myMap = function(callback, thisArg) {
  if (typeof callback !== 'function') throw new TypeError(callback + ' is not a function');
  const result = [];
  for (let i = 0; i < this.length; i++) {
    if (i in this) { // Handles sparse arrays
      result[i] = callback.call(thisArg, this[i], i, this);
    }
  }
  return result;
};

// Test:
console.log([1, 2, 3].myMap(x => x * 2)); // [2, 4, 6]
```

---

### Q2: Custom Polyfill for `Array.prototype.filter()`
```javascript
Array.prototype.myFilter = function(callback, thisArg) {
  if (typeof callback !== 'function') throw new TypeError(callback + ' is not a function');
  const result = [];
  for (let i = 0; i < this.length; i++) {
    if (i in this && callback.call(thisArg, this[i], i, this)) {
      result.push(this[i]);
    }
  }
  return result;
};

// Test:
console.log([1, 2, 3, 4, 5].myFilter(x => x % 2 === 0)); // [2, 4]
```

---

### Q3: Custom Polyfill for `Array.prototype.reduce()`
```javascript
Array.prototype.myReduce = function(callback, initialValue) {
  if (typeof callback !== 'function') throw new TypeError(callback + ' is not a function');
  const arr = this;
  let startIndex = 0;
  let accumulator;

  if (arguments.length >= 2) {
    accumulator = initialValue;
  } else {
    // Find first non-empty slot
    while (startIndex < arr.length && !(startIndex in arr)) {
      startIndex++;
    }
    if (startIndex >= arr.length) throw new TypeError('Reduce of empty array with no initial value');
    accumulator = arr[startIndex++];
  }

  for (let i = startIndex; i < arr.length; i++) {
    if (i in arr) {
      accumulator = callback(accumulator, arr[i], i, arr);
    }
  }
  return accumulator;
};

// Test:
console.log([1, 2, 3, 4].myReduce((acc, curr) => acc + curr, 0)); // 10
```

---

### Q4: Debounce Implementation (with Immediate Option)
```javascript
function debounce(fn, delay, immediate = false) {
  let timerId = null;

  return function(...args) {
    const context = this;
    const callNow = immediate && !timerId;

    clearTimeout(timerId);

    timerId = setTimeout(() => {
      timerId = null;
      if (!immediate) fn.apply(context, args);
    }, delay);

    if (callNow) {
      fn.apply(context, args);
    }
  };
}
```

---

### Q5: Throttle Implementation (Leading & Trailing Support)
```javascript
function throttle(fn, limit) {
  let inThrottle = false;
  let lastArgs = null;
  let lastContext = null;

  return function(...args) {
    if (!inThrottle) {
      fn.apply(this, args);
      inThrottle = true;

      setTimeout(() => {
        inThrottle = false;
        if (lastArgs) {
          fn.apply(lastContext, lastArgs);
          lastArgs = null;
          lastContext = null;
        }
      }, limit);
    } else {
      lastArgs = args;
      lastContext = this;
    }
  };
}
```

---

### Q6: Deep Clone Implementation (Handling Circular References)
```javascript
function deepClone(obj, hash = new WeakMap()) {
  if (obj === null || typeof obj !== 'object') return obj;
  if (obj instanceof Date) return new Date(obj);
  if (obj instanceof RegExp) return new RegExp(obj);
  if (hash.has(obj)) return hash.get(obj); // Cycle protection

  const clone = Array.isArray(obj) ? [] : Object.create(Object.getPrototypeOf(obj));
  hash.set(obj, clone);

  for (const key of Reflect.ownKeys(obj)) {
    clone[key] = deepClone(obj[key], hash);
  }
  return clone;
}

// Test Circular:
const a = { name: "Node" };
a.self = a;
const b = deepClone(a);
console.log(b.name, b.self === b); // "Node", true
```

---

### Q7: Generic Memoization Helper
```javascript
function memoize(fn) {
  const cache = new Map();

  return function(...args) {
    const key = JSON.stringify(args);
    if (cache.has(key)) {
      return cache.get(key);
    }
    const result = fn.apply(this, args);
    cache.set(key, result);
    return result;
  };
}

// Test:
const slowFactorial = n => (n <= 1 ? 1 : n * slowFactorial(n - 1));
const fastFactorial = memoize(slowFactorial);
console.log(fastFactorial(5)); // 120 (cached for subsequent calls)
```

---

### Q8: `once()` Function Wrapper
```javascript
function once(fn) {
  let executed = false;
  let result;

  return function(...args) {
    if (!executed) {
      executed = true;
      result = fn.apply(this, args);
    }
    return result;
  };
}

const initializeDB = once(() => {
  console.log("Database connection established!");
  return { connected: true };
});

initializeDB(); // "Database connection established!"
initializeDB(); // (does nothing, returns cached result)
```

---

### Q9: Automatic Currying Function
```javascript
function curry(fn) {
  return function curried(...args) {
    if (args.length >= fn.length) {
      return fn.apply(this, args);
    } else {
      return function(...nextArgs) {
        return curried.apply(this, args.concat(nextArgs));
      };
    }
  };
}

const sum3 = (a, b, c) => a + b + c;
const curriedSum = curry(sum3);
console.log(curriedSum(1)(2)(3)); // 6
console.log(curriedSum(1, 2)(3)); // 6
console.log(curriedSum(1)(2, 3)); // 6
```

---

### Q10: Flatten Array Recursive & Iterative
```javascript
// Recursive:
function flattenArray(arr) {
  return arr.reduce((acc, item) => {
    return acc.concat(Array.isArray(item) ? flattenArray(item) : item);
  }, []);
}

// Iterative (Stack):
function flattenIterative(arr) {
  const stack = [...arr];
  const res = [];
  while (stack.length) {
    const next = stack.pop();
    if (Array.isArray(next)) {
      stack.push(...next);
    } else {
      res.push(next);
    }
  }
  return res.reverse();
}

console.log(flattenArray([1, [2, [3, [4]], 5]])); // [1, 2, 3, 4, 5]
```

---

### Q11: Find Frequency of Array Elements
```javascript
function getFrequency(arr) {
  return arr.reduce((acc, curr) => {
    acc[curr] = (acc[curr] || 0) + 1;
    return acc;
  }, {});
}

console.log(getFrequency(['apple', 'banana', 'apple', 'orange', 'banana', 'apple']));
// { apple: 3, banana: 2, orange: 1 }
```

---

### Q12: Custom Promise Implementation (A+ Spec Compliant Subset)
```javascript
const PENDING = 'PENDING';
const FULFILLED = 'FULFILLED';
const REJECTED = 'REJECTED';

class MyPromise {
  constructor(executor) {
    this.status = PENDING;
    this.value = undefined;
    this.reason = undefined;
    this.onFulfilledCallbacks = [];
    this.onRejectedCallbacks = [];

    const resolve = (value) => {
      if (this.status === PENDING) {
        this.status = FULFILLED;
        this.value = value;
        this.onFulfilledCallbacks.forEach(fn => fn());
      }
    };

    const reject = (reason) => {
      if (this.status === PENDING) {
        this.status = REJECTED;
        this.reason = reason;
        this.onRejectedCallbacks.forEach(fn => fn());
      }
    };

    try {
      executor(resolve, reject);
    } catch (err) {
      reject(err);
    }
  }

  then(onFulfilled, onRejected) {
    onFulfilled = typeof onFulfilled === 'function' ? onFulfilled : val => val;
    onRejected = typeof onRejected === 'function' ? onRejected : err => { throw err; };

    return new MyPromise((resolve, reject) => {
      const handleFulfilled = () => {
        queueMicrotask(() => {
          try {
            const x = onFulfilled(this.value);
            resolve(x);
          } catch (err) {
            reject(err);
          }
        });
      };

      const handleRejected = () => {
        queueMicrotask(() => {
          try {
            const x = onRejected(this.reason);
            resolve(x);
          } catch (err) {
            reject(err);
          }
        });
      };

      if (this.status === FULFILLED) handleFulfilled();
      else if (this.status === REJECTED) handleRejected();
      else {
        this.onFulfilledCallbacks.push(handleFulfilled);
        this.onRejectedCallbacks.push(handleRejected);
      }
    });
  }

  catch(onRejected) {
    return this.then(null, onRejected);
  }
}
```
