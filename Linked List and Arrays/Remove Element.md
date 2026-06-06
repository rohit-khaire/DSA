# Remove all the Occurrences of Element from The Array

Nums is a vector and val is a value which is to be deleted from the vector

[LeetCode](https://leetcode.com/problems/remove-element/)

## OPTIMAL SOLUTION that beats 100% with 0ms

- Point prev to -1
- Start iterating the vector/array
- if anywhere nums[i]!=val, store the nums[i] at position ++prev ( nums[++prev]=nums[i] )
- If nums[i]==val, don't do anything and just move ahead

```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        if(nums.empty()) return 0;
        int prev=-1;
        for(int i=0;i<nums.size();i++){
            if(nums[i]!=val){
                nums[++prev]=nums[i];
            }
        }
        return prev+1;
    }
};
```

**TC=O(N) and SC=O(1)**
