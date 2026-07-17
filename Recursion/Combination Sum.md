# Combination Sum

[LeetCode](https://leetcode.com/problems/combination-sum/description/)

Given an array of distinct integers candidates and a target integer target, return a list of all unique combinations of candidates where the chosen numbers sum to target. You may return the combinations in any order.


The same number may be chosen from candidates an unlimited number of times. Two combinations are unique if the frequency of at least one of the chosen numbers is different.


Input: candidates = [2,3,6,7], target = 7

Output: [[2,2,3],[7]]

Explanation:

2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.

7 is a candidate, and 7 = 7.

These are the only two combinations.

# Approach - Recursive

Similar DP

We try all the possible paths

- We Recusrively call the helper function, we provide it

1) Array containing numbers
2) Current index within array arr, we will be working with the element at that index
3) Target which is to be achieved, to keep track of sum of elements is ds we just change the target, like instead of caluculating sum of elements in ds we just pass next target as CurrentTarget-arr[index]
4) ds which will be list to keep track of elements in current path, we store this list in result array if target becomes zero
5) res array (vector<vector<int>>) will be storing final result

- Our base case is when we go ahead of the last index (even when target is achieved before last index, then we just don't pick any element, but we end up only when we go ahead of last index)
  - If at this time target becomes 0, means we got the result list
  - return (If target is achieved, we store the ds as result, else we didn't find it)
- If current element (arr[index]) is <= target, then pick it
  - Then only we can pick it
  - pick it by adding it to list ds and calling the helper function with target as target-arr[index]
  - We pop last element from ds, so that we can get the result for no picking the current element
- We don't pick current element and move to next index, helper(arr,index+1,target,ds,res);

## CODE:


```cpp
class Solution {
public:
    void helper(vector<int> &arr, int index, int target, vector<int> &ds,vector<vector<int>> &res){
        if(index==arr.size()){//reached at end of arr array
            if(target==0){
                res.push_back(ds);
            }
            return;
        }
        if(arr[index]<=target){//Pick up the current element
            ds.push_back(arr[index]);
            helper(arr,index,target-arr[index],ds,res);
            ds.pop_back(); // As for current scenario, we added the extra element by picking it, now for not picking, we remove it
        }
        helper(arr,index+1,target,ds,res); //Called for next index, as we not picked index th element (Maybe it have pciked once) 
    }
    vector<vector<int>> combinationSum(vector<int>& arr, int target) {
        vector<vector<int>> ans;
        vector<int> ds; //To store elements in the solution till now
        helper(arr,0,target,ds,ans);
        return ans;
    }
};
```
