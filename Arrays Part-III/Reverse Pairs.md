# Reverse Pairs

Problem Statement: Given an array of numbers, you need to return the count of reverse pairs. <br> Reverse Pairs are those pairs where i<j and arr[i]>2*arr[j].

## Brute Force : Time Limit Exceeds for large input

The naive approach is pretty straightforward. We will use nested loops to generate all possible pairs. We know index i must be smaller than index j. So, we will fix i at one index at a time through a loop, and with another loop, we will check(the condition a[i] > 2*a[j]) the elements from index i+1 to N-1  if they can form a pair with a[i].

Note: For a better understanding of intuition, please watch the video at the bottom of the page.

Approach:

The steps are as follows:

First, we will run a loop(say i) from 0 to N-1 to select the a[i]. 

As index j should be greater than index i, inside loop i, we will run another loop i.e. j from i+1 to N-1, and select the element a[j].

Inside this second loop, we will check if a[i] > 2*a[j] i.e. if a[i] and a[j] can be a pair. If they satisfy the condition, we will increase the count by 1.

Finally, we will return the count i.e. the number of such pairs.

```cpp
class Solution {
public:
    int reversePairs(vector<int>& arr) {
        int n= arr.size();
        int cnt =0;
        for(int i=0;i<=n-2;i++){
            for(int j=i+1;j<n;j++){
                if((long long)arr[i]>2LL*arr[j]) cnt++;
            }
        }
        return cnt;
    }
};
```

**But this gives Time Limit Exceed Error**

**TC = O(N^2) and SC=O(1)**

> *For n = 50,000, that's about 1.25 billion comparisons, which will definitely TLE (Time Limit Exceed)*

# Optimal : Merge Sort + Two Pointers




