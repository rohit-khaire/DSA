# Remove Duplicates from Sorted Array

Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same.

[LeetCode](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)

## Brute Force using Set

- Use a set to store the elements of array
- iterate set and array simultaneously and store elements of set in Array
- While set is not empty of (it!=st.end)

```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        set<int>s(nums.begin(),nums.end());
        nums.clear();
        for(int x:s){
            nums.push_back(x);
        }

        return nums.size();
        
    }
};
```

TC=O(N) and SC=O(N)

## OPTIMAL using 2 pointers

> NO need of counter, use index to return no. of uniques

- Begin at the first position, which will always be part of the final unique list.
- Move through the list one item at a time, comparing the current item with the most recently kept unique item.
- If the current item is the same as the last kept one, skip it because it’s a duplicate.
- If it’s different, place it right after the last kept unique item to keep all unique values grouped at the front.
- Continue until every element in the list has been checked. The first part of the list now contains all the unique values in their original order, and the rest can be ignored.

```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if(nums.empty()) return 0;
        int n= nums.size(),prev=0;
        for(int i=1;i<n;i++){
            if(nums[i]!=nums[prev]){
                nums[++prev]=nums[i];
            }
        }
        return prev+1;
    }
};
```

TC=O(N) and SC=O(1)
