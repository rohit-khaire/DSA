# Climbing Stairs

It's a problem with hidden Fibonacci pattern inside it 

Given Integer N, now return how many ways you can reach N by taking 1 step 0r 2 step

[Leetcode](https://leetcode.com/problems/climbing-stairs/)

Example:

- Input: n = 2
- Output: 2


Explanation: There are two ways to climb to the top.

1. 1 step + 1 step
2. 2 steps

Example 2:

- Input: n = 3
- Output: 3
- Explanation: There are three ways to climb to the top.


1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step


# Approach - Using Fibonacci Iterative

Tried Recursive way, but without memoization, it's getting Time Limit Exceed

- If n<=2, return n
- make prev1=1 and prev2=2
- Now start fibonacci series
- return nTH value


```cpp
class Solution {
public:
    int climbStairs(int n) {
        //fibonacci problem
        if(n<=2) return n;
        int prev1=1;
        int prev2=2; //prev1 < prev2 < curr 
        for(int i=3;i<=n;i++){
            int curr = prev1+prev2;
            prev1=prev2;
            prev2=curr;
        }
        return prev2;
    }
};
```

TC:O(N) & SC:O(1)
