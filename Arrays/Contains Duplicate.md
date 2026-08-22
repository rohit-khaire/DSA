# Contains Duplicate

[Leetcode](https://leetcode.com/problems/contains-duplicate/)

Given an array of Integers. This array may contain duplicate element, if Duplicate element is present, then return True. Else False.

# Approach - TC:O(N^2)

Using Two points to search for current element in whole array. 

TC:O(N^2) & SC:O(1)

# Approach - Hash Set

Use a hash set (unordered) to check if current element is repeating or not. If current element exists in the set, we return True, as it's repeated.

```cpp
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_set<int> seen;

        for (int x : nums) {
            if (seen.count(x))
                return true;

            seen.insert(x);
        }

        return false;
    }
};
```

TC:O(N) & SC:O(N)


# Approach - Sorting

Sort the array, and check for repeated element.

```cpp
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        sort(nums.begin(), nums.end());

        for (int i = 1; i < nums.size(); i++) {
            if (nums[i] == nums[i - 1])
                return true;
        }

        return false;
    }
};
```

TC:O(N logN + N) & SC:O(1)
