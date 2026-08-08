# Missing Number

[Leetcode](https://leetcode.com/problems/missing-number/)

Given an array of numbers ranging from [0 to N] including 0 and N, where N is size of Array

Now provide one missing Number from the array.

# Approach - using XOR

The key property of XOR:

- x ^ x = 0
- x ^ 0 = x

We XOR: 

```cpp
n ^ 0 ^ 1 ^ 2 ^ ... ^ (n-1)
```


Example:

```cpp
nums = [3, 0, 1]

n = 3

ans = 3
ans ^= 0 ^ 3
ans ^= 1 ^ 0
ans ^= 2 ^ 1

Remaining = 2
```

- Get the size of Array
- Store ans=N
- start iterating from 0 to N-1
  - ans = ans XOR nums[i] XOR i
- return ans

# Code

```cpp
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int n = nums.size();
        int ans = n; //as N can also be answer, when N cannot be answer, we use nums[0]
        for(int i=0;i<n;i++){
            ans = ans ^ i ^ nums[i]; //cancels each other
        }
        return ans;
    }
};
```

Complexity:

- Time: O(n)
- Space: O(1)
