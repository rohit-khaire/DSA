# Valid Triangle Number

[Leetcode](https://leetcode.com/problems/valid-triangle-number/)

Given an integer array nums, return the number of triplets chosen from the array that can make triangles if we take them as side lengths of a triangle.

# Approach - using 2 pointers and third pointer is last limit for 2nd pointer (This don't allows right pointer to go further)

Can Visualize: [ChaiVisuals](https://dsa.chaicode.com/two-pointers/valid-triangle-number)

```cpp
class Solution {
public:
    int triangleNumber(vector<int>& nums) {
        sort(nums.begin(), nums.end());

        int n = nums.size();
        int ans = 0;

        for (int k = n - 1; k >= 2; k--) {
            int i = 0;
            int j = k - 1;

            while (i < j) {
                if (nums[i] + nums[j] > nums[k]) {
                    ans += (j - i);
                    j--;
                } else {
                    i++;
                }
            }
        }

        return ans;
    }
};
```


## Complexity
- Sorting: O(n log n)
- Two pointers: O(n^2)
- Overall: O(n^2)
- Space: O(1) (ignoring the sorting implementation's internal space)
