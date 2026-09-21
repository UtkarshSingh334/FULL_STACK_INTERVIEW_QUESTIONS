# 🧩 DSA - Easy Questions

> **Topics Covered:** Big-O Complexity Analysis, Two Pointers Technique, Sliding Window, Reverse Linked List, Valid Parentheses (Stack), Binary Search ($O(\log n)$), Palindrome Check, Maximum Subarray (Kadane's Algorithm).

---

### Q1: Big-O Asymptotic Notation
**Question:** Explain Big-O notation, Time Complexity, and Space Complexity. Rank common complexities from best to worst.

**Answer:**
Big-O describes the upper bound limiting behavior of an algorithm's execution time or memory space as the input size $n$ grows toward infinity.

**Complexity Ranking (Best to Worst):**
$O(1) < O(\log n) < O(n) < O(n \log n) < O(n^2) < O(2^n) < O(n!)$

---

### Q2: Two Pointers: Two Sum II (Sorted Array)
**Question:** Given a 1-indexed sorted integer array, find two numbers that add up to a target number in $O(n)$ time and $O(1)$ extra space.

```javascript
function twoSumSorted(numbers, target) {
  let left = 0;
  let right = numbers.length - 1;

  while (left < right) {
    const sum = numbers[left] + numbers[right];
    if (sum === target) {
      return [left + 1, right + 1];
    } else if (sum < target) {
      left++;
    } else {
      right--;
    }
  }
  return [];
}
console.log(twoSumSorted([2, 7, 11, 15], 9)); // [1, 2]
```

---

### Q3: Stacks: Valid Parentheses
**Question:** Given a string containing `'('`, `')'`, `'{'`, `'}'`, `'['`, `']'`, determine if the input string is valid using a Stack.

```javascript
function isValidParentheses(s) {
  const stack = [];
  const map = { ')': '(', '}': '{', ']': '[' };

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
console.log(isValidParentheses("()[]{}")); // true
console.log(isValidParentheses("(]"));      // false
```

---

### Q4: Linked Lists: Reverse a Singly Linked List
**Question:** Reverse a singly linked list iteratively in $O(n)$ time and $O(1)$ space.

```javascript
class ListNode {
  constructor(val = 0, next = null) {
    this.val = val;
    this.next = next;
  }
}

function reverseList(head) {
  let prev = null;
  let curr = head;

  while (curr !== null) {
    let nextTemp = curr.next;
    curr.next = prev;
    prev = curr;
    curr = nextTemp;
  }
  return prev;
}
```

---

### Q5: Kadane's Algorithm (Maximum Subarray Sum)
**Question:** Find the contiguous subarray with the largest sum in an array with negative and positive numbers in $O(n)$ time.

```javascript
function maxSubArray(nums) {
  let currentSum = nums[0];
  let maxSum = nums[0];

  for (let i = 1; i < nums.length; i++) {
    currentSum = Math.max(nums[i], currentSum + nums[i]);
    maxSum = Math.max(maxSum, currentSum);
  }
  return maxSum;
}
console.log(maxSubArray([-2, 1, -3, 4, -1, 2, 1, -5, 4])); // 6 (Subarray [4, -1, 2, 1])
```
---

### Q6: Missing Number in Array ($1$ to $n$)
**Question:** How do you find the single missing number in an array containing numbers from $1$ to $n$?

**Answer:**
Calculate expected arithmetic series sum $rac{n 	imes (n + 1)}{2}$ and subtract actual array sum.

```cpp
#include <iostream>
using namespace std;

int findMissingNumber(int arr[], int size, int n) {
    int expectedSum = n * (n + 1) / 2;
    int actualSum = 0;
    for (int i = 0; i < size; i++) {
        actualSum += arr[i];
    }
    return expectedSum - actualSum;
}

int main() {
    int arr[] = {1, 2, 3, 5};
    int n = 5;
    cout << "Missing number: " << findMissingNumber(arr, 4, n); // 4
    return 0;
}
```
- **Time Complexity:** $O(n)$
- **Space Complexity:** $O(1)$

---

### Q7: Check Prime Number ($O(\sqrt{n})$)
**Question:** How do you check whether an integer $n$ is prime efficiently?

**Answer:**
A prime number is greater than 1 with exactly two divisors (1 and itself). Test divisors up to $\sqrt{n}$.

```cpp
#include <iostream>
using namespace std;

bool isPrime(int n) {
    if (n < 2) return false;
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) return false;
    }
    return true;
}

int main() {
    int n = 17;
    cout << (isPrime(n) ? "Prime" : "Not Prime") << endl; // Prime
    return 0;
}
```
- **Time Complexity:** $O(\sqrt{n})$
- **Space Complexity:** $O(1)$

---

### Q8: Armstrong Number Check
**Question:** What is an Armstrong number and how do you verify one?

**Answer:**
An Armstrong number (for 3 digits) is a number equal to the sum of the cubes of its digits (e.g. $153 = 1^3 + 5^3 + 3^3 = 1 + 125 + 27 = 153$).

```cpp
#include <iostream>
using namespace std;

bool isArmstrong(int n) {
    int original = n;
    int sum = 0;
    while (n > 0) {
        int digit = n % 10;
        sum += (digit * digit * digit);
        n /= 10;
    }
    return sum == original;
}

int main() {
    int n = 153;
    cout << (isArmstrong(n) ? "Armstrong Number" : "Not an Armstrong Number") << endl;
    return 0;
}
```

---

### Q9: Recursion: Factorial of a Number
**Question:** What is recursion? Calculate the factorial of $n$ recursively.

**Answer:**
Recursion is when a function calls itself to solve smaller subproblems, terminating at a base case.

```cpp
#include <iostream>
using namespace std;

int factorial(int n) {
    if (n <= 1) return 1; // Base case
    return n * factorial(n - 1); // Recursive step
}

int main() {
    cout << "Factorial of 5: " << factorial(5) << endl; // 120
    return 0;
}
```

---

### Q10: Fibonacci Series Iterative
**Question:** Generate the first $n$ numbers of the Fibonacci sequence in $O(n)$ time and $O(1)$ space.

```cpp
#include <iostream>
using namespace std;

void printFibonacci(int n) {
    int a = 0, b = 1;
    for (int i = 0; i < n; i++) {
        cout << a << " ";
        int next = a + b;
        a = b;
        b = next;
    }
    cout << endl;
}

int main() {
    printFibonacci(10); // 0 1 1 2 3 5 8 13 21 34
    return 0;
}
```

---

### Q11: Reverse an Array (Two Pointers)
**Question:** Reverse an array in-place using the two pointers approach.

```cpp
#include <iostream>
using namespace std;

void reverseArray(int arr[], int n) {
    int left = 0, right = n - 1;
    while (left < right) {
        swap(arr[left], arr[right]);
        left++;
        right--;
    }
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    reverseArray(arr, 5);
    for (int i = 0; i < 5; i++) cout << arr[i] << " "; // 5 4 3 2 1
    return 0;
}
```

---

### Q12: Swap Two Variables Without a Third Variable
**Question:** How do you swap two variables without using a temporary third variable?

**Answer:**
```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 10, b = 20;

    // Arithmetic approach
    a = a + b; // a = 30
    b = a - b; // b = 10
    a = a - b; // a = 20

    cout << "a: " << a << ", b: " << b << endl; // a: 20, b: 10

    // In modern C++, std::swap(a, b) is preferred to avoid integer overflow:
    swap(a, b);
    return 0;
}
```
