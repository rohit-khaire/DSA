# Sum of Square Numbers


[LeetCode](https://leetcode.com/problems/sum-of-square-numbers/)

Given a non-negative integer c, decide whether there're two integers a and b such that ``a^2 + b^2 = c`` .

# Approach 

- We take square root of C
- Now we point Left to 0 and Right to Square root of C
- Now, we treat Left as A and Right as B
- Calculate A^2 + B^2
- If this result is Equals to C, we return True
- Else if, result is > C , right--
- else left++
- So our result comes under these left and right if exists (Initially between 0 and sqrt(C)), and we reduce this range one by one

```cpp
class Solution {
public:
    bool judgeSquareSum(int c) {
        long long right = sqrt(c);
        long long left = 0;
        while(left<=right){
            long long res = left*left + right*right;
            if(res==c) return true;
            else if(res>c) right--;
            else left++;
        }
        return false;
    }
};
```

