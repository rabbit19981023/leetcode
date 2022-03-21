# 7. Reverse Integer: Medium

## Description

Given a signed 32-bit integer `x`, return `x` with its digits reversed.

If reversing `x` causes the value to go outside the signed 32-bit integer range `[-2^31, 2^31 - 1]`, then return `0`.

**Assume the environment does not allow you to store 64-bit integers (signed or unsigned).**

```
Given:
  int x

Output:
  int result
```

### Constraints

```
-2^31 <= result <= 2^31 - 1
```

## Examples

### Example 01

```
Input: x = 123
Output: 321
```

### Example 02

```
Input: x = -123
Output: -321
```

### Example 03

```
Input: x = 120
Output: 21
```

## Solution

### Python

```python
class Solution:
# main func
  def reverse(self, x: int) -> int:
    result = 0

    while x != 0:
      last_num = self.get_last_num(x)

      if x < 10 and x > -10 and self.is_overflow(result, last_num):
        result = 0
        break

      result = result * 10 + last_num
      x = self.remove_last_num(x)

    return result

# utils
  def math_trunc(self, a, b):
    num = a / b
    if (num >= 0): return a // b
    if (num < 0): return a // (b * -1 ) * -1

  def math_mod(self, a, b):
    remainder = a - b * self.math_trunc(a, b)
    return remainder

  def is_overflow(self, result, last_num):
    MAX = 2 ** 31 - 1
    MIN = -2 ** 31

    if result > 0:
      LIMIT = self.math_trunc(MAX, 10)
      if result > LIMIT: return True
      if result == LIMIT and last_num > 7: return True

    if result < 0:
      LIMIT = self.math_trunc(MIN, 10)
      if result < LIMIT: return True
      if result == LIMIT and last_num < -8: return True

    return False

  def get_last_num(self, x):
    return self.math_mod(x, 10)

  def remove_last_num(self, x):
    return self.math_trunc(x, 10)
```

### C++

```cpp
class Solution {
public:
// main func
  int reverse(int x);

// utils
  bool isOverflow(int result, int lastNum);
  int getLastNum(int x);
  int removeLastNum(int x);
};

int Solution::reverse(int x) {
  int result = 0;

  while (x != 0) {
    int lastNum = getLastNum(x);

    if (x < 10 && x > -10 && isOverflow(result, lastNum)) {
      result = 0;
      break;
    }

    result = result * 10 + lastNum;
    x = removeLastNum(x);
  }

  return result;
}

bool Solution::isOverflow(int result, int lastNum) {
  if (result > 0) {
    int LIMIT = INT_MAX / 10;
    if (result > LIMIT) return true;
    if (result == LIMIT && lastNum > 7) return true;
  }

  if (result < 0) {
    int LIMIT = INT_MIN / 10;
    if (result < LIMIT) return true;
    if (result == LIMIT && lastNum < -8) return true;
  }

  return false;
}

int Solution::getLastNum(int x) {
  return x % 10;
}

int Solution::removeLastNum(int x) {
  return x / 10;
}
```
