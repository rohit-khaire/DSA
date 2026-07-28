# Find Minimum in Rotated Sorted Array

[Leetcode](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/)

Given an array which is firstly sorted and then it's rotated. We need to return first element of Array (i.e. Element which was first element nums[0] when Array was sorted, before rotations).

Array is [3,5,1]

1) Sorted => [1,3,5]
2) Rotated K times => [5,1,3]

& This rotated array is given to us

Return first element of Sorted Array(i.e. 1)

# Approach - Binary Search

- We apply Binary search but with few things different, as array is sorted and then rotated
- Point left to 0th index and right to N-1 th index
- Loop While(left<right)
  - get the mid index
  - if element at this middle position is Greater than nums[right], we just move need to search in right half, so left=mid+1
  - else our solution exists in left half or current mid may be pointing to answer, hence we do right=mid
- Left elements points to answer

```cpp
class Solution {
public:
    int findMin(vector<int>& nums) {
        int left=0;
        int right=nums.size()-1;
        while(left<right){
            int mid = left+ ((right-left)/2); //in even case, left is wala is mid
            if(nums[mid]>nums[right]){
                left=mid+1;
            }else{
                right=mid; //as current element can also be answer
            }
        }
        return nums[left];
    }
};
```

TC: O(logN) and SC:O(1)
