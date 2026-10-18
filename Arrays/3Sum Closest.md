[Leetcode](https://leetcode.com/problems/3sum-closest/)

# 🔥 3Sum Closest — Sort + Two Pointers | O(n²) Optimal Solution 🚀

## 💡 Intuition
Why check every possible triplet when Two Pointers can do the job efficiently?

The trick is simple:
1. **Sort the array** to make the Two Pointer approach work.
2. Fix one element `i` and initialize `left = i + 1` and `right = n - 1`.
3. Calculate the sum of these three elements and update `closest` if the current sum is nearer to the target.
4. If the sum is smaller than the target, move `left++` to increase it. If larger, move `right--` to decrease it.
5. If the sum equals the target, return immediately!

## 💻 C++ Code
```cpp
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        int n = nums.size();
        sort(nums.begin(), nums.end());

        int closest = nums[0] + nums[1] + nums[2];

        for (int i = 0; i < n - 2; i++) {
            int left = i + 1, right = n - 1;

            while (left < right) {
                int currSum = nums[i] + nums[left] + nums[right];

                if (abs(target - currSum) < abs(target - closest)) {
                    closest = currSum;
                }

                if (currSum < target) {
                    left++;
                } else if (currSum > target) {
                    right--;
                } else {
                    return currSum;
                }
            }
        }

        return closest;
    }
};
```

## ⏱️ Complexity Analysis
- **Time Complexity:** O(n²) — Sorting takes O(n log n), followed by nested loops using Two Pointers.
- **Auxiliary Space:** O(1), excluding sorting implementation details.

## 🧠 Key Takeaway
**Fix one element + Two Pointers + Track the closest sum.**

Instead of storing the difference, always store the actual sum closest to the target. That's the key to solving this problem correctly!
