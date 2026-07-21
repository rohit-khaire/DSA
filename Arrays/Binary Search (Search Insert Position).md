# Search Insert Position

[LeetCode](https://leetcode.com/problems/search-insert-position/description/)

Apply Binary Search

```cpp
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int n = nums.size();
        int left = 0, right=n-1;
        while(left<=right){
            int mid = left + ((right- left) / 2);
            if(nums[mid]==target){
                return mid;
            }
            if(nums[mid]<target){
                left = mid+1;
            }else{
                right = mid-1;
            }
        }
        return left;
    }
};
```

TC:O(logN) and SC: O(1)
