# 3 Sum 

[LeetCode](https://leetcode.com/problems/3sum/description/)

Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

In solution, I can change the target.

Notice that the solution set must not contain duplicate triplets.

## Brute Force

Using 3 loops and getting elements and performing necessary calculations

**TC = O(N^3)**

## Better is using 2 loops (Gives TLE )

Use two loops and check that if required(more) value is present in HashSet or not

2nd loop(j) will store the elements(in HashSet) while moving further, so that the more element can be searched in that HashSet

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        set<vector<int>> res;
        int n=nums.size();
        int target = 0;
        for(int i=0;i<n;i++){
            unordered_set<int> st;
            for(int j=i+1;j<n;j++){
                long long thirdEle = target - nums[i];
                thirdEle -= nums[j];
                if(st.count(thirdEle)){
                    vector<int> temp = {nums[i],nums[j],(int)thirdEle};
                    sort(temp.begin(),temp.end());
                    res.insert(temp);
                }
                st.insert(nums[j]);
            }
        }
        return vector<vector<int>>(res.begin(),res.end());
    }
};
```
**TC=O(N^2+MlogM) = Worst M = N^2 => O(N^2+N^2 log(N^2)) => N^2 log(N)**

**SC=O(N^2)**

## Optimal (For Sorted Array)

Sort the Array

**Using 1 Loops and using 2 pointers**

### Algorithm (Sort + Fix + Two Pointers)

1. **Sort** the array.
2. **Fix one element** `i` (first number of triplet).
3. Skip duplicate `i`.
4. Use **two pointers**:

   * `j = i + 1` (left)
   * `k = n - 1` (right)
5. Calculate `sum = nums[i] + nums[j] + nums[k]`.
6. If:

   * `sum == 0` → store triplet, move both pointers, skip duplicates.
   * `sum < 0` → increase sum ⇒ `j++`. until j<k and nums[j]==nums[j-1]
   * `sum > 0` → decrease sum ⇒ `k--`. until j<k and nums[k]==nums[k+1]
7. Continue until `j < k`.

---

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        int target=0;  // As I eish to create a general solution
        int n=nums.size();
        vector<vector<int>> res;
        sort(nums.begin(), nums.end());
        for(int i=0;i<n;i++){
            if(i>0 && nums[i]==nums[i-1]) continue;
            int j = i+1;
            int k = n-1;
            while(j<k){
                long long sum = nums[i];
                sum+=nums[j];
                sum+=nums[k];
                if(sum==target){
                    res.push_back({nums[i],nums[j],nums[k]});
                    j++;
                    k--;
                    while(j<k && nums[j]==nums[j-1]) j++;
                    while(j<k && nums[k]==nums[k+1]) k--;
                }
                else if(sum<target){
                    j++;
                    while(j<k && nums[j]==nums[j-1]) j++;
                }
                else{
                    k--;
                    while(j<k && nums[k]==nums[k+1]) k--;
                }
            }
        }
        return res;
    }
};
```

**Time Complexity:** `O(N²)`
**Space Complexity:** `O(1)` (excluding output array)

