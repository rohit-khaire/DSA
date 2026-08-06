# Maximum Average Subarray I

[LeetCode](https://leetcode.com/problems/maximum-average-subarray-i/description/)

Given an array, and integer K, K is window size, find maximum average possible using k size window


# Approach - Sliding Window (Find Max sum and then get it's avg)

- Compute the sum of the first k elements.
- Store it as the current maximum sum.
- Move the window one element at a time:
- Add the new element entering the window.
- Remove the element leaving the window.
- Update the maximum sum.
- Return maxSum / k as a double.


```cpp
class Solution {
public:
    double findMaxAverage(vector<int>& nums, int k) {
        int n = nums.size();

        long long windowSum = 0;

        // First window
        for (int i = 0; i < k; i++) {
            windowSum += nums[i];
        }

        long long maxSum = windowSum;

        // Slide the window
        for (int i = k; i < n; i++) {
            windowSum += nums[i] - nums[i - k];
            maxSum = max(maxSum, windowSum);
        }

        return (double)maxSum / k;
    }
};
```

TC:O(N) & SC:O(1)
