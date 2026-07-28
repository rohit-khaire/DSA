# Search in Rotated Sorted Array

[Leetcode](https://leetcode.com/problems/search-in-rotated-sorted-array/description/)

Given arrays is sorted but has rotated multiple times.

Now we need to search element in it using Binary Search. Search the Target element in this Array and return it's index.

# Approach - Binary Search

When we get mid, we check which is half is sorted 

[4,5,6,7,0,1,2]

mid = 7

Left half : [4,5,6,7]   -> Sorted

Right half: [0,1,2]     -> Rotated

We always check that can target lie in that sorted part? If yes, then search there, else search in opposite half


- Point left to 0 and right to N-1
- while(left<=right)
  - get the mid
  - check if element at index mid is == target, if yes then return mid
  - check if left half is sorted?
    - can our target lie in it? Between nums[left] to nums[mid]
    - If yes then make right=mid-1; else make left=mid+1
  - Else right half is sorted
    - Check that, can my target lie in that sorted part?
    - If yes then search in it, by making left=mid+1 ; else right=mid-1
- Return -1, as no Target found in Array

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int left=0;
        int right=nums.size()-1;
        while(left<=right){
            int mid = left+(right-left)/2;
            if(nums[mid]==target) return mid;
            // search for sorted part, is left part sorted?
            if(nums[left]<=nums[mid]){
//                 [4,5,6,7,0,1,2]
//                  mid = 7
                    // Left half : [4,5,6,7]   -> Sorted
                    // Right half: [0,1,2]     -> Rotated
                    //Check If answer can be in sorted half
                    if(target<nums[mid] && target>=nums[left]){
                        //search in left part, which is sorted
                        right=mid-1;
                    }else{
                        left=mid+1;
                    }
            }
            //else right half is sorted
            // if(nums[mid]<nums[right]){
            else{
                if(target>nums[mid] && target<=nums[right]){
                    left=mid+1;
                }else{
                    right=mid-1;
                }
            }
        }
        return -1;
    }
};
```

TC:O(logN) and SC:O(1)
