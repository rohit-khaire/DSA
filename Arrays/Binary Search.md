# Binary Search

Pure binary search TC:O(logN)

[Leetcode](https://leetcode.com/problems/binary-search/)

# Approach - Two pointer


This is the **standard Binary Search algorithm** for searching an element in a **sorted array**.

**Input:** Sorted array `nums`, target element `target`
**Output:** Index of `target`, or `-1` if not found.

1. Initialize two pointers:

   * `low = 0`
   * `high = n - 1`

2. Repeat while `low <= high`:

   * Calculate the middle index:
     `mid = low + (high - low) / 2`
   * If `nums[mid] == target`, return `mid`.
   * If `nums[mid] < target`, the target can only be in the **right half**, so set:
     `low = mid + 1`
   * Otherwise, the target can only be in the **left half**, so set:
     `high = mid - 1`

3. If the loop ends, the target does not exist in the array. Return `-1`.



```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int high = nums.size()-1;
        int low =0;
        while(low<=high){
            int mid = low + (high-low)/2;
            if(nums[mid]==target) return mid;
            else if(nums[mid]<target){
                low = mid+1;
            }else{
                high = mid-1;
            }
        }
        return -1;
    }
};
```

TC:O(logN) and SC:O(1)
