[Leetcode](https://leetcode.com/problems/count-commas-in-range/description/)

# Solution

Intuition

A comma is added to every number starting from 1,000.

So, for a given n:

- If n < 1000, there are no commas.
- If n >= 1000, every number from 1000 through n contains one comma.


Therefore, the total number of commas is simply the count of integers in the range [1000, n], which is:

n - 999.

Approach:

- Check if n is less than 1000.
- If yes, return 0.
- Otherwise, calculate n - 999.
- Return the result.

```cpp
class Solution {
public:
    int countCommas(int n) {
        if(n<1000) return 0;
        else return n-999;
    }
};
```
