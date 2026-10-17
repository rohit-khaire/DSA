# 🚀 O(1) Range Sum Queries! The Prefix Sum Trick You Must Know 🔥

[Leetcode](https://leetcode.com/problems/range-sum-query-immutable/description/)

## 💡 Approach: Prefix Sum

Instead of calculating the sum from scratch for every query, we precompute prefix sums in the constructor.

**The key formula:**

`sumRange(left, right) = prefix[right + 1] - prefix[left]`

### 💻 C++ Solution

```cpp
class NumArray {
    vector<int> prefix;

public:
    NumArray(vector<int>& nums) {
        prefix.resize(nums.size() + 1, 0);

        for (int i = 0; i < nums.size(); i++) {
            prefix[i + 1] = prefix[i] + nums[i];
        }
    }

    int sumRange(int left, int right) {
        return prefix[right + 1] - prefix[left];
    }
};
```

### 🧠 Example

`nums = [-2, 0, 3, -5, 2, -1]`

Prefix Sum Array:

`prefix = [0, -2, -2, 1, -4, -2, -3]`

Query: `sumRange(2, 5)`

`prefix[6] - prefix[2]`

`= -3 - (-2) = -1`

**Output: -1**

### ⚡ Complexity Analysis

- **Constructor:** O(n)
- **Each sumRange query:** O(1)
- **Extra Space:** O(n)

### 🔑 Why Does This Work?

`prefix[i]` stores the sum of the first `i` elements.

Subtracting `prefix[left]` from `prefix[right + 1]` removes the sum of all elements before `left`, leaving only the required range.

**Remember:** Precompute once, answer every query in constant time! 🚀
