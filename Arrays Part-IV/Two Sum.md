# Two Sum

[LeetCode](https://leetcode.com/problems/two-sum/)

Problem Statement: Given an array of integers arr[] and an integer target.

1st variant: Return YES if there exist two numbers such that their sum is equal to the target. Otherwise, return NO.

2nd variant: Return indices of the two numbers such that their sum is equal to the target. Otherwise, we will return {-1, -1}.

Return 2 indices (i,j) from array, whose sum of eles at that positions is Equal to Target

You assume that each input would have **exactly one solution** , and you may not use the same element twice.

## Brute Force : Direct 2 Loops

You start to iterate whole array with i, and iterate i+1 to n-1 with j, creating combination of (i,j) as

```
n=4
(i,j) =>
(0,1)
(0,2)
(0,3)
(1,2)
(1,3)
(2,3)

And each time you match sum of values at that indices and value of target (arr[i]+arr[j])== target
```

CODE:

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& arr, int target) {
        int n = arr.size();
        for( int i=0;i<n;i++){
            for(int j=i+1;j<n;j++){
                if((arr[i]+arr[j])== target){
                    return {i,j};
                }
            }
        }
        return {};
    }
};
```

**TC = O(N^2) and SC=O(1)**

## Better : Use HashMap

Using a unordered HashMap to store {element,index} so that whenever we iterate the array, we calculate target-arr[i] to get the number which we require, if that number exists in the HashMap, we can say that we got the answer

<br>

``mpp.find(7)`` => searches for key 7

It returns an iterator.

When found: points to 7

If not found: it points to end of map, mpp.end()

Why not ``if(mpp[more])`` used as if more not found, then it creates a one with 0 as value

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int,int> mpp;
        for(int i=0;i<nums.size();i++){
            int a=nums[i];
            int more= target-a;
            if(mpp.find(more) != mpp.end()){
                return {i,mpp[more]};
            }
            mpp[a]=i;
        }
        return {-1,-1};
    }
};
```


**TC = O(N) and SC=O(N)**



## Optimal : Only for sorted array, when no indices are required

Good for YES or NO solution, as sorting array would lead to loss of indices, and if any data structure using will lead to increase in SC

```cpp
string twoSum(vector<int>& nums, int target){
    sort(nums.begin(),nums.end());
    int high=nums.size()-1;
    int low=0;
    while(low<high){
        if(nums[low]+nums[high]==target){ // can also int sum = nums[low] + nums[high];
            return "YES";
        }
        else if(nums[low]+nums[high] > target){
            high--;
        }
        else if(nums[low]+nums[high] < target){ // Can use else
            low++;
        }
    }
    return "NO";
}
```

**TC=Time Complexity: O(N log N) due to sorting the array initially, where N is the number of elements. The two-pointer traversal runs in O(N).**

**Space Complexity: O(1)**

