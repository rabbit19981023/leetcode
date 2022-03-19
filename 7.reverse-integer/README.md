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
    sign = -1 if self.isNegative(x) else 1
    _x = abs(x)
    while _x != 0:
      lastNum = self.getLastNum(_x)

      if _x < 10 and self.isOverFlow(result, lastNum, sign):
        result = 0
        break

      result = result * 10 + lastNum
      _x = self.removeLastNum(_x)

    return result * sign

# utils func
  def isOverFlow(self, result, lastNum, sign):
    # for positive int: max = 2 ** 31 - 1
    # for negative int: min = -2 ** 31
    LIMIT = (2 ** 31) // 10

    if result > LIMIT: return True
    if result == LIMIT:
      if sign > 0 and lastNum > 7: return True
      if sign < 0 and lastNum > 8: return True
    return False

  def isNegative(self, x):
    return x < 0

  def getLastNum(self, x):
    return x % 10

  def removeLastNum(self, x):
    return x // 10
```
