# Product of Array Except Self

[Leetcode](https://leetcode.com/problems/product-of-array-except-self/description/)

Given an array. Return answer array of same size, where answer[i] is equal to the product of all the elements of nums except nums[i].

Example:

Input: nums = [1,2,3]

Output: [6,3,2]

Cannot use Division Operator, complete in O(N) TC

# Approach - Precompute left prefix product & right as postfix product

TC: O(3N) & SC:O(3N)

We use the **Prefix Product * Suffix Product** approach.

### Algorithm (Extra Space Approach)

1. Let `n` be the size of the array.
2. Create three arrays of size `n`:

   * `left[]` → stores the product of all elements to the **left** of each index, except self.
   * `right[]` → stores the product of all elements to the **right** of each index, except self.
   * `ans[]` → stores the final answer as left[i]*right[i].
3. Initialize:

   * `left[0] = 1` (no element exists to the left of the first element).
   * `right[n-1] = 1` (no element exists to the right of the last element).
4. Traverse from **left to right** to fill `left[]`:

   * `left[i] = left[i-1] * nums[i-1]`
5. Traverse from **right to left** to fill `right[]`:

   * `right[i] = right[i+1] * nums[i+1]`
6. For every index `i`, compute:

   * `ans[i] = left[i] * right[i]`
7. Return `ans`.


```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        vector<int> ans(n);
        vector<int> left(n);
        left[0]=1;
        for(int i=1;i<n;i++){
            left[i]=left[i-1]*nums[i-1];
        }
        vector<int> right(n);
        right[n-1]=1;
        for(int i=n-2;i>=0;i--){
            right[i]=right[i+1]*nums[i+1];
        }
        for(int i=0;i<n;i++){
            ans[i]=left[i]*right[i];
        }
        return ans;
    }
};
```


