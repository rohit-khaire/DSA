# Max Consecutive Ones

Given a binary array nums, return the maximum number of consecutive 1's in the array.

[LeetCode](https://leetcode.com/problems/max-consecutive-ones/description/)

## Solution Beats 100% with 0ms

- Have cnt to count the sequence size and have ``maxCnt`` to have maximum length count for sequence of Ones to return as Answer
- ``maxCnt`` stores the maximum streak found so far.
- Start traversing the Array
- if nums[i]==0 means our sequence gets broken here, make cnt=0
- If nums[i]==1 means increase the cnt and store maxCnt as max from maxCnt and cnt
- return maxCnt as the solution

```cpp
class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums) {
        int cnt=0;
        int maxCnt=0;
        for(int i=0;i<nums.size();i++){
            if(nums[i]==0){
                cnt=0;
            }
            else{
                cnt++;
                maxCnt=max(maxCnt,cnt);
            }
        }
        return maxCnt;
    }
};
```

TC=O(N) and SC=O(1)
