# 💡 DSA - Medium Interview Questions & Solutions

---

### Q1: Valid Parentheses (Stack)
**Problem:** Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['`, and `']'`, determine if the input string is valid.
- Open brackets must be closed by the same type of brackets.
- Open brackets must be closed in the correct order.

```javascript
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
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(N)$

---

### Q2: Happy Number (Floyd's Cycle Detection)
**Problem:** A happy number is defined by replacing the number by the sum of the squares of its digits repeatedly until the number equals 1, or it loops endlessly in a cycle which does not include 1.

```javascript
function isHappy(n) {
  function getNext(num) {
    let sum = 0;
    while (num > 0) {
      const digit = num % 10;
      sum += digit * digit;
      num = Math.floor(num / 10);
    }
    return sum;
  }

  // Floyd's Tortoise and Hare Cycle-Finding Algorithm
  let slow = n;
  let fast = getNext(n);

  while (fast !== 1 && slow !== fast) {
    slow = getNext(slow);
    fast = getNext(getNext(fast));
  }

  return fast === 1;
}

console.log(isHappy(19)); // true (19 -> 82 -> 68 -> 100 -> 1)
console.log(isHappy(2));  // false (trapped in 4 -> 16 -> 37 -> 58 -> 89 -> 145 -> 42 -> 20 -> 4...)
```
- **Time Complexity:** $O(\log N)$
- **Space Complexity:** $O(1)$

---

### Q3: Best Time to Buy and Sell Stock (Single Pass)
**Problem:** You are given an array `prices` where `prices[i]` is the price of a given stock on the $i^{\text{th}}$ day. You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

```javascript
function maxProfit(prices) {
  if (!prices || prices.length < 2) return 0;

  let minPrice = Infinity;
  let maxProfit = 0;

  for (const price of prices) {
    if (price < minPrice) {
      minPrice = price; // Update lowest buy price seen so far
    } else if (price - minPrice > maxProfit) {
      maxProfit = price - minPrice; // Update maximum profit
    }
  }

  return maxProfit;
}

console.log(maxProfit([7, 1, 5, 3, 6, 4])); // 5 (Buy at 1, Sell at 6)
console.log(maxProfit([7, 6, 4, 3, 1]));    // 0 (No profit possible)
```
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$

---

### Q4: Fibonacci Sequence (Iterative, Recursive, Dynamic Programming)
**Problem:** Return the $N^{\text{th}}$ Fibonacci number where $F(0) = 0$, $F(1) = 1$, and $F(N) = F(N-1) + F(N-2)$.

```javascript
// 1. Space-Optimized Iterative: O(N) Time, O(1) Space (Best)
function fibonacci(n) {
  if (n <= 1) return n;
  let prev2 = 0;
  let prev1 = 1;
  for (let i = 2; i <= n; i++) {
    const current = prev1 + prev2;
    prev2 = prev1;
    prev1 = current;
  }
  return prev1;
}

// 2. Top-Down Memoization (DP): O(N) Time, O(N) Space
function fibMemo(n, memo = {}) {
  if (n in memo) return memo[n];
  if (n <= 1) return n;
  return memo[n] = fibMemo(n - 1, memo) + fibMemo(n - 2, memo);
}

// 3. Naive Recursive: O(2^N) Time (Exponential - Avoid in production)
function fibRecursive(n) {
  if (n <= 1) return n;
  return fibRecursive(n - 1) + fibRecursive(n - 2);
}

console.log(fibonacci(10)); // 55
```

---

### Q5: Sliding Window Technique (Fixed & Dynamic Windows)
**Problem 1 (Fixed Window):** Maximum Sum Subarray of Size $K$.
```javascript
function maxSubarraySum(arr, k) {
  if (arr.length < k) return null;
  let maxSum = 0;
  let windowSum = 0;

  // Initialize first window
  for (let i = 0; i < k; i++) windowSum += arr[i];
  maxSum = windowSum;

  // Slide window
  for (let i = k; i < arr.length; i++) {
    windowSum += arr[i] - arr[i - k];
    maxSum = Math.max(maxSum, windowSum);
  }
  return maxSum;
}

console.log(maxSubarraySum([2, 1, 5, 1, 3, 2], 3)); // 9 ([5, 1, 3])
```

**Problem 2 (Dynamic Window):** Longest Substring Without Repeating Characters.
```javascript
function lengthOfLongestSubstring(s) {
  const charMap = new Map(); // char -> last seen index
  let maxLength = 0;
  let left = 0;

  for (let right = 0; right < s.length; right++) {
    const char = s[right];
    if (charMap.has(char) && charMap.get(char) >= left) {
      left = charMap.get(char) + 1; // Shrink window past duplicate
    }
    charMap.set(char, right);
    maxLength = Math.max(maxLength, right - left + 1);
  }

  return maxLength;
}

console.log(lengthOfLongestSubstring("abcabcbb")); // 3 ("abc")
console.log(lengthOfLongestSubstring("pwwkew"));   // 3 ("wke")
```
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(\min(N, M))$ where $M$ is alphabet size

---

### Q6: Substring Problems (Generation & Matching)
**Problem 1:** Generate all possible continuous substrings of a string.
```javascript
function getAllSubstrings(str) {
  const result = [];
  for (let i = 0; i < str.length; i++) {
    for (let j = i + 1; j <= str.length; j++) {
      result.push(str.slice(i, j));
    }
  }
  return result;
}

console.log(getAllSubstrings("abc")); // ["a", "ab", "abc", "b", "bc", "c"]
```
- **Total substrings for string of length $N$:** $\frac{N(N+1)}{2} = O(N^2)$

**Problem 2:** Implement `isSubstring(text, pattern)` without built-in methods.
```javascript
function isSubstring(text, pattern) {
  if (!pattern) return 0;
  const n = text.length;
  const m = pattern.length;

  for (let i = 0; i <= n - m; i++) {
    let match = true;
    for (let j = 0; j < m; j++) {
      if (text[i + j] !== pattern[j]) {
        match = false;
        break;
      }
    }
    if (match) return i; // Found at index i
  }
  return -1;
}

console.log(isSubstring("hello world", "world")); // 6
```

---

### Q7: Rotate Array by K Positions (In-Place Reversal)
**Problem:** Rotate array right by $K$ steps in $O(N)$ time and $O(1)$ space.

```javascript
function rotateArray(nums, k) {
  k = k % nums.length;

  function reverse(arr, start, end) {
    while (start < end) {
      [arr[start], arr[end]] = [arr[end], arr[start]];
      start++;
      end--;
    }
  }

  reverse(nums, 0, nums.length - 1); // 1. Reverse all
  reverse(nums, 0, k - 1);           // 2. Reverse first k
  reverse(nums, k, nums.length - 1); // 3. Reverse rest

  return nums;
}

console.log(rotateArray([1, 2, 3, 4, 5, 6, 7], 3)); // [5, 6, 7, 1, 2, 3, 4]
```

---

### Q8: Flatten a Nested Array (Recursion vs Stack)
**Problem:** Given a multi-dimensional array with arbitrary nesting depth, flatten it into a 1D array.

```javascript
// Approach 1: Recursive (O(N) Time, O(D) Depth Space)
function flattenArrayRecursive(arr) {
  const result = [];

  function helper(subArr) {
    for (const item of subArr) {
      if (Array.isArray(item)) {
        helper(item);
      } else {
        result.push(item);
      }
    }
  }

  helper(arr);
  return result;
}

// Approach 2: Iterative with Depth Parameter (Custom Polyfill)
function flattenToDepth(arr, depth = 1) {
  if (depth <= 0) return arr.slice();
  
  return arr.reduce((acc, curr) => {
    if (Array.isArray(curr)) {
      acc.push(...flattenToDepth(curr, depth - 1));
    } else {
      acc.push(curr);
    }
    return acc;
  }, []);
}

console.log(flattenArrayRecursive([1, [2, [3, [4, 5]]], 6])); // [1, 2, 3, 4, 5, 6]
console.log(flattenToDepth([1, [2, [3, 4]]], 1));              // [1, 2, [3, 4]]
```
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(D)$ where $D$ is maximum nesting depth

