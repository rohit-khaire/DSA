# First Missing Positive

[LeetCode](https://leetcode.com/problems/first-missing-positive/description/)

Given an unsorted integer array nums. Return the smallest positive integer that is not present in nums.

## Approach - TC:O(2N) & SC:O(1)

Arrays should be like:

Index 0 : 1

Index 1 : 2

Index 2 : 3

- Start iterating the array
- If current value is between 1 & n
  - get it's correct position, as ith index stores i+1 value, so swap it with with it's correct position
  - do not move i
- move i, i++
- Again start iterating the array
  - If currentValue is not equals to i+1, return i+1 as missing
- return n+1 as missing


```cpp
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        int n = nums.size();
        int i = 0;

        while (i < n) {
            if (nums[i] >= 1 && nums[i] <= n) {
                int correctPos = nums[i] - 1;

                if (nums[i] != nums[correctPos]) {
                    swap(nums[i], nums[correctPos]);
                    continue;
                }
            }
            i++;
        }

        for (int i = 0; i < n; i++) {
            if (nums[i] != i + 1)
                return i + 1;
        }

        return n + 1;
    }
};
```
