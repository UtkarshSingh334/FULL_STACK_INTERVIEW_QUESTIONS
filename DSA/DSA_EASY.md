# 💡 DSA - Easy Interview Questions & Solutions

---

### Q1: Swap Two Variables Without a 3rd Variable
**Problem:** Swap the values of two variables `a` and `b` in $O(1)$ space without using a temporary variable.

**Approaches:**
1. **Bitwise XOR (Best)**: Doesn't suffer from arithmetic overflow.
2. **Arithmetic (+ / -)**: Works for numbers, but risks integer overflow for large numbers.
3. **ES6 Destructuring**: Modern JavaScript clean syntax.

```javascript
// 1. Bitwise XOR Approach
function swapXOR(a, b) {
  a = a ^ b;
  b = a ^ b;
  a = a ^ b;
  return [a, b];
}

// 2. Arithmetic Approach
function swapArithmetic(a, b) {
  a = a + b;
  b = a - b;
  a = a - b;
  return [a, b];
}

// 3. ES6 Destructuring
function swapDestructuring(a, b) {
  [a, b] = [b, a];
  return [a, b];
}

console.log(swapXOR(10, 20)); // [20, 10]
```
- **Time Complexity:** $O(1)$
- **Space Complexity:** $O(1)$

---

### Q2: Check if a Number is Prime
**Problem:** Determine if a given positive integer $N > 1$ is prime in optimal $O(\sqrt{N})$ time.

**Intuition:**
A number $N$ is prime if it has no divisors other than $1$ and $N$. All primes greater than 3 can be written in the form $6k \pm 1$. We only need to check factors up to $\lfloor\sqrt{N}\rfloor$.

```javascript
function isPrime(n) {
  if (n <= 1) return false;
  if (n <= 3) return true;
  if (n % 2 === 0 || n % 3 === 0) return false;

  // Check 6k ± 1 divisors up to sqrt(n)
  for (let i = 5; i * i <= n; i += 6) {
    if (n % i === 0 || n % (i + 2) === 0) return false;
  }
  return true;
}

console.log(isPrime(2));  // true
console.log(isPrime(29)); // true
console.log(isPrime(49)); // false (7 * 7)
```
- **Time Complexity:** $O(\sqrt{N})$
- **Space Complexity:** $O(1)$

---

### Q3: Check if a Number is an Armstrong Number
**Problem:** An Armstrong number (narcissistic number) is a number that equals the sum of its own digits each raised to the power of the total number of digits.
- Example: $153 \rightarrow 1^3 + 5^3 + 3^3 = 1 + 125 + 27 = 153$ (True)
- Example: $9474 \rightarrow 9^4 + 4^4 + 7^4 + 4^4 = 6561 + 256 + 2401 + 256 = 9474$ (True)

```javascript
function isArmstrong(num) {
  if (num < 0) return false;
  const digits = String(num).split('').map(Number);
  const power = digits.length;
  const sum = digits.reduce((acc, digit) => acc + Math.pow(digit, power), 0);
  return sum === num;
}

console.log(isArmstrong(153));  // true
console.log(isArmstrong(9474)); // true
console.log(isArmstrong(123));  // false
```
- **Time Complexity:** $O(\log_{10} N)$
- **Space Complexity:** $O(1)$ auxiliary space

---

### Q4: Find the Largest Element in an Array
**Problem:** Find the maximum element in an unsorted array in $O(N)$ time.

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

console.log(findLargest([14, 58, 20, 77, 3, 99, 45])); // 99
```
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$

---

### Q5: Find the Second Largest Element in an Array (Single Pass)
**Problem:** Find the second largest distinct number in an array in a single traversal ($O(N)$ time, $O(1)$ space).

```javascript
function findSecondLargest(arr) {
  if (!arr || arr.length < 2) return null;

  let largest = -Infinity;
  let secondLargest = -Infinity;

  for (const num of arr) {
    if (num > largest) {
      secondLargest = largest;
      largest = num;
    } else if (num > secondLargest && num < largest) {
      secondLargest = num;
    }
  }

  return secondLargest === -Infinity ? null : secondLargest;
}

console.log(findSecondLargest([12, 35, 1, 10, 34, 1])); // 34
console.log(findSecondLargest([10, 10, 10]));           // null (No distinct 2nd largest)
```
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$

---

### Q6: Reverse a String (Multiple Approaches)
**Problem:** Reverse a given string.

```javascript
// Approach 1: In-Place Two Pointers (O(N) Time, O(1) Extra Auxiliary Space)
function reverseString(str) {
  const chars = str.split('');
  let left = 0, right = chars.length - 1;
  while (left < right) {
    [chars[left], chars[right]] = [chars[right], chars[left]];
    left++;
    right--;
  }
  return chars.join('');
}

// Approach 2: Built-in Methods
const reverseBuiltIn = (str) => str.split('').reverse().join('');

console.log(reverseString("javascript")); // "tpircsavaj"
```
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$ auxiliary

---

### Q7: Factorial of a Number (Iterative & Recursive)
**Problem:** Compute $N! = N \times (N-1) \times \dots \times 1$.

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
  if (n === 0 || n === 1) return 1; // Base case
  return n * factorialRecursive(n - 1);
}

console.log(factorialIterative(5)); // 120
console.log(factorialRecursive(6)); // 720
```

---

### Q8: Find Missing Number in Array `[1..N]`
**Problem:** Given an array containing $N-1$ distinct integers in the range $[1, N]$, find the single missing number in $O(N)$ time and $O(1)$ space.

```javascript
// Approach 1: Bitwise XOR (No Integer Overflow)
function findMissingXOR(arr, n) {
  let xorAll = 0;
  let xorArr = 0;

  for (let i = 1; i <= n; i++) xorAll ^= i;
  for (const num of arr) xorArr ^= num;

  return xorAll ^ xorArr;
}

// Approach 2: Sum Formula (N * (N + 1) / 2)
function findMissingSum(arr, n) {
  const expectedSum = (n * (n + 1)) / 2;
  const actualSum = arr.reduce((acc, curr) => acc + curr, 0);
  return expectedSum - actualSum;
}

console.log(findMissingXOR([1, 2, 4, 5, 6], 6)); // 3
```
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$

---

### Q9: Recursion Fundamentals
**Problem:** Explain what recursion is, its base condition, call stack unwinding, and implement recursive sum of digits.

**Concept:**
Recursion is when a function calls itself to solve a smaller subproblem until it reaches a **Base Case** (termination condition) to prevent a stack overflow (`RangeError: Maximum call stack size exceeded`).

```javascript
// Sum of Digits using Recursion
// e.g. 1234 -> 1 + 2 + 3 + 4 = 10
function sumOfDigits(n) {
  if (n === 0) return 0; // Base condition
  return (n % 10) + sumOfDigits(Math.floor(n / 10)); // Recursive call
}

console.log(sumOfDigits(1234)); // 10
```
