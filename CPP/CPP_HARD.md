# ⚡ C++ - DSA Solutions for Questions From Notes (Hard)

> **Topics from Notes Covered:** Flatten Array / Nested Structure with Stack, Sliding Window (Longest Substring Without Repeating Characters).

---

### Q1: Longest Substring Without Repeating Characters (C++)
```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
using namespace std;

int lengthOfLongestSubstring(string s) {
  vector<int> lastIndex(256, -1);
  int maxLen = 0, left = 0;

  for (int right = 0; right < s.length(); right++) {
    if (lastIndex[s[right]] >= left) {
      left = lastIndex[s[right]] + 1;
    }
    lastIndex[s[right]] = right;
    maxLen = max(maxLen, right - left + 1);
  }
  return maxLen;
}
```

---

### Q2: Flatten Multi-Level Data Structure with Stack (C++)
```cpp
#include <iostream>
#include <vector>
#include <stack>
#include <variant>
using namespace std;

// Representing nested array elements using std::variant
struct NestedElement;
using Element = variant<int, vector<NestedElement>>;
struct NestedElement {
  Element val;
};

vector<int> flatten(const vector<NestedElement>& nested) {
  vector<int> result;
  stack<NestedElement> st;

  for (auto it = nested.rbegin(); it != nested.rend(); ++it) {
    st.push(*it);
  }

  while (!st.empty()) {
    NestedElement curr = st.top();
    st.pop();

    if (holds_alternative<int>(curr.val)) {
      result.push_back(get<int>(curr.val));
    } else {
      const auto& sub = get<vector<NestedElement>>(curr.val);
      for (auto it = sub.rbegin(); it != sub.rend(); ++it) {
        st.push(*it);
      }
    }
  }

  return result;
}
```
