# Concatenate Non-Zero Digits and Multiply by Sum I

[LeetCode](https://leetcode.com/problems/concatenate-non-zero-digits-and-multiply-by-sum-i/description/?envType=daily-question&envId=2026-07-07)

Given one number n, ignore the zeros and create number ``x`` such that it contains the same number without any zeros in it. Get ``sum`` of all the digits in ``x`` , Multiply ``x*sum``


# Approach

- Get the last digit of number
- If it's not zero
  - create the number x from it, x= last*(pow(10,p))+x
  - Incerement p, p keeps track length of number x
  - Add the current digit to sum
  - Remove last digit from number
- return x*sum

<br>

```cpp
class Solution {
public:
    long long sumAndMultiply(int n) {
        if(n==0 || n==1) return n;
        int num = n;
        long long x = 0;
        long long sum=0;
        int p = 0;
        while(num){
            int last = num%10;
            if(last!=0){
                // x = x*10 + last;
                x = last*(pow(10,p)) + x;
                p++;
                sum+=last;
                
            }
            num/=10;
        }
        return x*sum;
    }
};
```

TC=O(N) and SC=O(1)
