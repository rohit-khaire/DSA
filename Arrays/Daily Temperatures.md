# Daily Temps

[Leetcode](https://leetcode.com/problems/daily-temperatures/)

Given an array of temperatures. We need to find a warmer temperatures for each temperature and return an answer array which contains the waiting time for warmer temperature.

Answer array has how many days to wait for a warmer temperature.

# Brute

For each temp, search for a warmer temp is available or not in i+1 to N elements


TC:O(N^2) and SC:O(1) ignoring answer array

# Optimal - Start from left to right and use Monotonic Stack

For each temperature, we check in stack that can my current temp be someone's warmer?

In monotonic stack we store index as we can calculate waiting time using indexes.

- We create an ans array with all elements as 0
- We start traversing for i=0 to N-1
  - For current temp, can it be a warmer for any previous temp?
  - Check in stack, stack's top is index, we check nums[st.top()], and we pop top while(!st.empty() && temps[st.top()]<temps[i]), and calculate and store waiting time for that removed index
  - Push current index
- return ans array 

```cpp
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& temps) {
        int n=temps.size();
        stack<int> st;
        vector<int> ans(n,0); //stores final ans
        for(int i=0;i<n;i++){
            while(!st.empty() && temps[st.top()]<temps[i]){ //for each element, checking that can you be someone's warmer
                ans[st.top()]=i-st.top(); //your(top's) warmer is me
                st.pop();
            }
            st.push(i);
        }
        return ans;

    }
};
```

TC:O(N) and SC:O(N) as using stack
