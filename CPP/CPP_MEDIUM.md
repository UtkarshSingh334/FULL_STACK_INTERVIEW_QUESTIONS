# ⚡ C++ - DSA Solutions for Questions From Notes (Medium)

> **Topics from Notes Covered:** Valid Parentheses, Happy Number, Buy and Sell Stock, Fibonacci, Sliding Window, Substrings, Rotate Array.

---

### Q1: Valid Parentheses (C++)
```cpp
#include <iostream>
#include <stack>
#include <unordered_map>
using namespace std;

bool isValid(string s) {
  stack<char> st;
  unordered_map<char, char> matching = {
    {')', '('},
    {'}', '{'},
    {']', '['}
  };

  for (char c : s) {
    if (c == '(' || c == '{' || c == '[') {
      st.push(c);
    } else {
      if (st.empty() || st.top() != matching[c]) return false;
      st.pop();
    }
  }
  return st.empty();
}
```

---

### Q2: Happy Number (C++)
```cpp
#include <iostream>
using namespace std;

int getNext(int n) {
  int sum = 0;
  while (n > 0) {
    int d = n % 10;
    sum += d * d;
    n /= 10;
  }
  return sum;
}

bool isHappy(int n) {
  int slow = n, fast = getNext(n);
  while (fast != 1 && slow != fast) {
    slow = getNext(slow);
    fast = getNext(getNext(fast));
  }
  return fast == 1;
}
```

---

### Q3: Best Time to Buy and Sell Stock (C++)
```cpp
#include <iostream>
#include <vector>
#include <climits>
using namespace std;

int maxProfit(const vector<int>& prices) {
  int minPrice = INT_MAX;
  int profit = 0;
  for (int p : prices) {
    if (p < minPrice) minPrice = p;
    else if (p - minPrice > profit) profit = p - minPrice;
  }
  return profit;
}
```

---

### Q4: Sliding Window Maximum Sum Subarray of Size K (C++)
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int maxSubarraySum(const vector<int>& arr, int k) {
  if (arr.size() < k) return -1;
  int windowSum = 0;
  for (int i = 0; i < k; i++) windowSum += arr[i];
  int maxSum = windowSum;

  for (size_t i = k; i < arr.size(); i++) {
    windowSum += arr[i] - arr[i - k];
    maxSum = max(maxSum, windowSum);
  }
  return maxSum;
}
```

---

### Q5: Rotate Array by K Steps in $O(1)$ Space (C++)
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

void rotateArray(vector<int>& nums, int k) {
  k %= nums.size();
  reverse(nums.begin(), nums.end());
  reverse(nums.begin(), nums.begin() + k);
  reverse(nums.begin() + k, nums.end());
}
```
