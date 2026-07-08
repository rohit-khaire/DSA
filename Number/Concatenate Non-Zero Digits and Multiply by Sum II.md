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

# Approach Optimal

- Keep calculate the values of of sum,x,powers and length of x. So that we can directly use the values from index, no need to calulate everything same things again and again.

<br>

<img width="568" height="235" alt="image" src="https://github.com/user-attachments/assets/6efff2b1-7362-453a-9af9-3146b9424dad" />

<br>

- We iterate the string one and calculate and store
  - Sum of prefix till now (Sum of elements till this index)
  - Created number of non-zeros till now (Concatinated numbers till this index), Later we can cut the left-right digits according to query index. Save in moded number
  - Number of Digits in X
- Powers of 10^___ , like on index 0 we can get 10^0=1

<br>

- Now we start generating answer
- Iterate all the elements in Queries, queries[i] has [lefti,righti]
  - Get l as queries[i][0] and r as queries[i][1]
  - Get rangeSum (Sum of digits from l to r) as prefixSum[r]-prefixSum[l-1]
  - Get rangeCount (Number of digits in x) as prefixCount[r]-prefixCount[l-1]
  - Get rangeNum (Non zero digits concatinated range from l to r) as prefixNum[r] - (prefNum[l-1] * pow10[cntRange] % MOD + MOD) % MOD;
  - Store in result as ans.push_back((rangeNum * rangeSum) % MOD);
- Return result matrix

<br>

```cpp
class Solution {
public:
    static const int MOD = 1000000007;
    vector<int> sumAndMultiply(string s, vector<vector<int>>& queries) {
        int n = s.size();
        vector<long long> prefSum(n);
        vector<long long> prefNum(n);
        vector<int> prefCnt(n);
        vector<long long> pow10(n + 1);
        pow10[0] = 1;

        for (int i = 1; i <= n; i++)
            pow10[i] = (pow10[i - 1] * 10) % MOD;

        long long sum = 0;
        long long num = 0;
        int cnt = 0;

        for (int i = 0; i < n; i++) {

            if (s[i] != '0') {
                sum += s[i] - '0';
                cnt++;
                num = (num * 10 + (s[i] - '0')) % MOD;
            }

            prefSum[i] = sum;
            prefCnt[i] = cnt;
            prefNum[i] = num;
        }
        vector<int> ans;
        for (auto &q : queries) {
            int l = q[0];
            int r = q[1];
            long long rangeSum = prefSum[r];
            if (l > 0)
                rangeSum -= prefSum[l - 1];

            int cntRange = prefCnt[r];
            if (l > 0)
                cntRange -= prefCnt[l - 1];

            long long rangeNum = prefNum[r];

            if (l > 0) {
                rangeNum = (rangeNum - prefNum[l - 1] * pow10[cntRange] % MOD + MOD) % MOD;
            }

            ans.push_back((rangeNum * rangeSum) % MOD);
        }

        return ans;
    }
};
```



