# 1. Two Sum: Easy

## Description

```
Given:
  int[] nums
  int target

Result:
  int[2] result

Reason:
  result[0] + result[1] == target
```

## Examples

### Example 01

```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

### Example 02

```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

### Example 03

```
Input: nums = [3,3], target = 6
Output: [0,1]
```

## Solution

### Python

```python
class Solution:
  def twoSum(self, nums: List[int], target: int) -> List[int]:
    db = {}

    for i in range(len(nums)):
      current = nums[i]
      diff = target - current

      if (diff in db):
        partner_index = db[diff]
        return [partner_index ,i]

      db[current] = i
```

### C++

```cpp
class Solution {
public:
  vector<int> twoSum(vector<int>& nums, int target);
};

vector<int> Solution::twoSum(vector<int>& nums, int target) {
  map<int, int> db;

  for (int i = 0; i < nums.size(); i++) {
    int current = nums[i];
    int diff = target - current;

    if (db.find(diff) != db.end()) {
      int partner_index = db[diff];
      return {partner_index ,i};
    }

    db[current] = i;
  }

  return {0, 0};
}
```
