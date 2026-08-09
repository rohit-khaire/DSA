# Number of Bits

[Leetcode](https://leetcode.com/problems/number-of-1-bits/description/)


# Approach

```cpp
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int count = 0;

        while (n) {
            n &= (n - 1);  // Remove the rightmost 1-bit
            count++;
        }

        return count;
    }
};
```

