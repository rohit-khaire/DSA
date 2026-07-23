# K Largest Element 

[Leetcode](https://leetcode.com/problems/kth-largest-element-in-an-array/)

# Approach using Dutch national flag

Taking last element as Pivot. If normally it was taken, then at worst case it take O(N^2) which was leading to Time Limit Exceeded. Hence used Dutch National Flag.


```cpp
class Solution {
public:
    int partition(vector<int>& nums, int left, int right) {
        int pivot = nums[right];

        int i = left;
        int j = left;
        int k = right;

        while (j <= k) {
            if (nums[j] < pivot) {
                swap(nums[i], nums[j]);
                i++;
                j++;
            }
            else if (nums[j] > pivot) {
                swap(nums[j], nums[k]);
                k--;
            }
            else {
                j++;
            }
        }

        // Return starting index of equal elements
        return i;
    }

    int quickSelect(vector<int>& nums, int left, int right, int target) {
        while (left <= right) {

            int pivot = nums[right];

            int low = left;
            int mid = left;
            int high = right;

            // 3-way partition
            while (mid <= high) {
                if (nums[mid] < pivot) {
                    swap(nums[low], nums[mid]);
                    low++;
                    mid++;
                }
                else if (nums[mid] > pivot) {
                    swap(nums[mid], nums[high]);
                    high--;
                }
                else {
                    mid++;
                }
            }

            // Equal range is [low, high]
            if (target < low) {
                right = low - 1;
            }
            else if (target > high) {
                left = high + 1;
            }
            else {
                return nums[target];
            }
        }

        return -1;
    }

    int findKthLargest(vector<int>& nums, int k) {
        int n = nums.size();

        // kth largest -> (n-k)th smallest
        int target = n - k;

        return quickSelect(nums, 0, n - 1, target);
    }
};
```

TC:O(N) and SC:O(1)
