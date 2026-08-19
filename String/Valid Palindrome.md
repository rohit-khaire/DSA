# Valid Palindrome

[Leetcode](https://leetcode.com/problems/valid-palindrome/description/)


# Approach - Two Pointers

- left starts from the beginning.
- right starts from the end.
- Skip characters that aren't letters or digits using isalnum().
- Compare both characters after converting them to lowercase.
- If they differ → false.
- Move both pointers inward.
- If all characters match → true.

```cpp
class Solution {
public:
    bool isPalindrome(string s) {
        int left = 0;
        int right = s.size() - 1;

        while (left < right) {
            while (left < right && !isalnum(s[left]))
                left++;

            while (left < right && !isalnum(s[right]))
                right--;

            if (tolower(s[left]) != tolower(s[right]))
                return false;

            left++;
            right--;
        }

        return true;
    }
};
```

TC:O(N) & SC:O(1)
