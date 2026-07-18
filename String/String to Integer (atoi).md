# String to Integer (atoi)

[LeetCode](https://leetcode.com/problems/string-to-integer-atoi/description/)

Given a string

- Ignore white spaces
- Check the sign if present(+ or -), if not present means it's Positive
- If digit, then start creating the number
- if number is exceeding (INT_MAX-digit)/10, then return round number as INT_MAX if number is positive,else INT_MIN

# Approach - TC: O(N)

Approach is same as above

```cpp
class Solution {
public:
    int myAtoi(string s) {
        // return (s-'0');
        int i=0;
        int n=s.size();
        //remove white space
        while(i<n && s[i]==' '){
            i++;
        }
        //Check sign
        int sign=1; //1 means positive and -1 means negative
        if(i<n && (s[i]=='+' || s[i]=='-')){
            if(s[i]=='-'){
                sign=-1;
            }
            i++;
        }
        //atoi on actual Numbers, digit by digit
        long long ans=0;
        while(i<n && isdigit(s[i])){
            int digit= s[i]-'0';
            if (ans > (INT_MAX - digit) / 10) {
                return sign==1?INT_MAX:INT_MIN;
            }
            ans = ans*10 + digit;
            i++;
        }
        return (int) ans*sign;
    }
};
```

TC:O(N) & SC:O(1)
