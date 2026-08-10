# Find Smallest Letter Greater Than Target

[Leetcode](https://leetcode.com/problems/find-smallest-letter-greater-than-target/description/)

Given an Array of characters and it's in ascending order => 'a','b','c'

Target is a character, find smallest letter which is greater than Target

# Approach 

Perform Binary Search on array



```cpp
class Solution {
public:
    char nextGreatestLetter(vector<char>& letters, char target) {
        int left = 0, right = letters.size() - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            
            if (letters[mid] <= target)
                left = mid + 1;
            else
                right = mid - 1;
        }
        
        // If no letter is greater than target, wrap around
        return letters[left % letters.size()];
    }
};
```

TC:O(logN) & SC:O(1)
