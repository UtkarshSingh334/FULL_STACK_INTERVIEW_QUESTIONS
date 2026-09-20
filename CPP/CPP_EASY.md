# ⚡ C++ - DSA Solutions for Questions From Notes (Easy)

> **Topics from Notes Covered:** Swap Without 3rd Variable, Prime Number, Armstrong Number, Missing Number, Largest Element, Second Largest Element, Reverse String, Factorial, Recursion.

---

### Q1: Swap Two Numbers Without 3rd Variable (C++)
```cpp
#include <iostream>
using namespace std;

void swapXOR(int &a, int &b) {
  a = a ^ b;
  b = a ^ b;
  a = a ^ b;
}

int main() {
  int a = 10, b = 20;
  swapXOR(a, b);
  cout << a << " " << b << endl; // 20 10
  return 0;
}
```

---

### Q2: Prime Number Check in $O(\sqrt{N})$ (C++)
```cpp
#include <iostream>
using namespace std;

bool isPrime(int n) {
  if (n <= 1) return false;
  if (n <= 3) return true;
  if (n % 2 == 0 || n % 3 == 0) return false;

  for (int i = 5; i * i <= n; i += 6) {
    if (n % i == 0 || n % (i + 2) == 0) return false;
  }
  return true;
}
```

---

### Q3: Armstrong Number Check (C++)
```cpp
#include <iostream>
#include <cmath>
#include <string>
using namespace std;

bool isArmstrong(int num) {
  if (num < 0) return false;
  string s = to_string(num);
  int power = s.length();
  int sum = 0, temp = num;

  while (temp > 0) {
    int digit = temp % 10;
    sum += pow(digit, power);
    temp /= 10;
  }
  return sum == num;
}
```

---

### Q4: Largest and Second Largest Element (C++)
```cpp
#include <iostream>
#include <vector>
#include <climits>
using namespace std;

pair<int, int> findLargestAndSecond(const vector<int>& arr) {
  int largest = INT_MIN;
  int second = INT_MIN;

  for (int x : arr) {
    if (x > largest) {
      second = largest;
      largest = x;
    } else if (x > second && x < largest) {
      second = x;
    }
  }
  return {largest, second};
}
```

---

### Q5: Reverse a String In-Place (C++)
```cpp
#include <iostream>
#include <string>
using namespace std;

void reverseString(string& s) {
  int left = 0, right = s.length() - 1;
  while (left < right) {
    swap(s[left++], s[right--]);
  }
}
```

---

### Q6: Factorial (Iterative & Recursive) (C++)
```cpp
#include <iostream>
using namespace std;

long long factorial(int n) {
  if (n <= 1) return 1;
  return n * factorial(n - 1);
}
```

---

### Q7: Find Missing Number in `[1..N]` (C++)
```cpp
#include <iostream>
#include <vector>
using namespace std;

int findMissing(const vector<int>& arr, int n) {
  int xorAll = 0, xorArr = 0;
  for (int i = 1; i <= n; i++) xorAll ^= i;
  for (int num : arr) xorArr ^= num;
  return xorAll ^ xorArr;
}
```
