# Longest Substring Without Repeating Character

[LeetCode](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

Just provide the maximum length of substr with no repeating characters in it

# Approach - 2 pointers and sliding window and hashing

- right keeps expanding the window.
- If a duplicate appears inside the current window, move left just past the previous occurrence of that repeated character.
- Update the character's latest index.
- Record the largest window size.


```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        vector<int> lastIndex(256, -1);
        int left = 0;
        int maxLength = 0;

        for (int right = 0; right < s.size(); right++) {
            if (lastIndex[s[right]] >= left) {
                left = lastIndex[s[right]] + 1;
            }

            lastIndex[s[right]] = right;
            maxLength = max(maxLength, right - left + 1);
        }

        return maxLength;
    }
};
```

TC: O(N) and SC=O(256) we only need to hash characters only, so 26 size can also work by making 'a' to 0 in hash index

