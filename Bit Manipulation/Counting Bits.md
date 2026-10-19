[Leetcode](https://leetcode.com/problems/counting-bits/)

Return answer array where there are 0 to N indexes, where ans[i] = No. of 1s in binary representation of i

# `ans[i] = ans[i / 2] + (i % 2)`


## 💡 Intuition
What if I told you that you don't need to convert every number into binary to count its set bits? 🤯

The secret is that **the answer for a number can be calculated using the answer for a smaller number!**

## 🚀 Approach: Divide by 2
We use this simple formula:

`ans[i] = ans[i / 2] + (i % 2)`

- **`i / 2`** removes the last bit of the binary representation (integer division).
- **`i % 2`** tells us whether the number is odd or even.
  - Even → last bit is `0`, so add `0`.
  - Odd → last bit is `1`, so add `1`.

For example:
- `ans[6] = ans[3] + 0 = 2`
- `ans[7] = ans[3] + 1 = 3`

We reuse previously calculated answers instead of counting bits from scratch. That's the beauty of **Dynamic Programming!** 🔥

## 💻 Solution (C++)

```cpp
class Solution {
public:
    vector<int> countBits(int n) {
        vector<int> ans(n + 1);
        ans[0] = 0;

        for (int i = 1; i <= n; i++) {
            ans[i] = ans[i / 2] + (i % 2);
        }

        return ans;
    }
};
```

## ⚡ Complexity Analysis
- **Time Complexity:** `O(n)` — we calculate each answer exactly once.
- **Space Complexity:** `O(n)` — to store the answers.

## 🧠 Remember This Trick
**“Divide by 2 to remove the last bit; remainder tells you what you removed!”**

One formula. No binary conversion. No repeated counting. Just smart DP. 🚀

#LeetCode #Cpp #DynamicProgramming #DSA #CodingInterview
