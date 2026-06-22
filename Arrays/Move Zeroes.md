# Move Zeroes

[LeetCode](https://leetcode.com/problems/move-zeroes/)

Move j only after swap, so that j remains on same point when both i and j points to 0, AT that time i moves ahead and j remains there only.

Now i compares the new element, are you zero? No, then swap with j as it has zero, so zero remains at the end always

# Beats 100%

```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        for(int i=0,j=0;i<nums.size();i++){
            if(nums[i]!=0){
                swap(nums[i],nums[j]);
                j++;
            }
        }
    }
};
```

- TC: O(n) and SC: O(1)
