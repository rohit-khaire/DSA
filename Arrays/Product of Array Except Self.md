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


# Avoid Using Extra Space Approach

Store prefix in Ans vector, then start iterating from last and calculate ans[i] using suffix variable, update suffix

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        vector<int> ans(n, 1);

        // Store prefix products in ans[]
        for (int i = 1; i < n; i++) {
            ans[i] = ans[i - 1] * nums[i - 1];
        }

        // Multiply with suffix products
        int suffix = 1;
        for (int i = n - 1; i >= 0; i--) {
            ans[i] *= suffix;
            suffix *= nums[i];
        }

        return ans;
    }
};
```


TC:O(2N) and SC:O(N)


# If Division Operator is Allowed

Array may contain zero, which can lead to every product as 0. If no zero in Array.

### Case 1: No zero

- Compute the product of all elements.

- For each index i, set:

```cpp
ans[i] = totalProduct / nums[i]
```

### Case 2: Zero in Array

1. Only One zero in Array

- Compute the product of all non-zero elements.
- Only the index containing 0 gets that product.
- Every other index gets 0.

```cpp
[1, 2, 0, 4] => [0, 0, 8, 0]
```


2. More than one Zero

Example:

[1, 2, 0, 4, 0]  => [0,0,0,0,0]

Every answer is 0.



 
