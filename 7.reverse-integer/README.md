# 7. Reverse Integer: Medium

## Description

Given a signed 32-bit integer `x`, return `x` with its digits reversed.

If reversing `x` causes the value to go outside the signed 32-bit integer range `[-2^31, 2^31 - 1]`, then return `0`.

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
  def reverse(self, x: int) -> int:
    result = 0
    sign = 1

    if (self.isNegative(x)):
      sign *= -1

    x = abs(x)
    for i in reversed(range(self.getDigits(x))):
      result += self.getLastNum(x) * 10 ** i
      x = self.removeLastNum(x)

    if (self.isNotValid(result, sign)):
      result = 0

    return result * sign

  def isNotValid(self, result, sign):
    if (sign > 0):
      return result >= 2 ** 31

    if (sign < 0):
      return result > 2 ** 31

  def isNegative(self, x):
    return x < 0

  def getDigits(self, x):
    length = 0
    
    while x > 0:
      length += 1
      x = x // 10

    return length

  def getLastNum(self, x):
    return x % 10

  def removeLastNum(self, x):
    return x // 10
```
