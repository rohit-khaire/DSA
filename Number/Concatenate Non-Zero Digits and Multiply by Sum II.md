# Concatenate Non-Zero Digits and Multiply by Sum II

[LeetCode](https://leetcode.com/problems/concatenate-non-zero-digits-and-multiply-by-sum-ii/description/?envType=daily-question&envId=2026-07-08)

Given string s, and 2D vector of Mx2 named as queries

Iterate through each query inside Queries, it contains two numbers [l,r] which represents substring from index l to r in string s

Get this substring, & create ``x`` which contains all the non-zero numbers, create ``sum`` which contains sum of all the non-zero numbers

At last return the ``x*sum`` but this value may exceed integer and can lead to integer overflow, hence mod it with 1000000007 or 10^9+7 

# Brute Force - Time Limit Exceeds

```cpp
class Solution {
public:
    vector<int> sumAndMultiply(string s, vector<vector<int>>& queries) {
        long long sum =0;
        vector<int> res;
        string x = "";
        for(int i=0;i<queries.size();i++){
            string sub = s.substr(queries[i][0], queries[i][1] - queries[i][0] + 1);
            for(char j: sub){
                if(j!='0'){
                    x+=j;
                    sum+= j-'0';
                }
            }
            long long num = 0;
            for(char c : x)
                num = (num * 10 + (c - '0')) % 1000000007;
            res.push_back((num*sum)%(1000000007));
            x="";
            sum=0;
        }
        return res;
    }
};
```

Time Limit Exceeds for large numbers

