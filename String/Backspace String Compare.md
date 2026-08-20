# Backspace String Compare 

[Leetcode](https://leetcode.com/problems/backspace-string-compare/)

Two strings are given ie. s & t

Both string contains ``#`` in between them.

``#`` means backspace was used, so previous character was deleted. 

Imagine a notepad where strings are typed, when # is used means backspace was used.

A ``#`` deletes the character immediately before it. 

# Approach - Use pointer from last for matching

Instead of actually constructing the resulting strings, we can scan from the end and skip characters that are erased.

For each string, start from end:

- # => increase skip (count of skip)
- Normal character & skip > 0 → skip it and decrease skip
- Otherwise → this is the next valid character



<br>

```cpp
class Solution {
public:
    bool backspaceCompare(string s, string t) {
        int i = s.size() - 1;
        int j = t.size() - 1;

        while (i >= 0 || j >= 0) {
            int Sskip = 0;
            int Tskip = 0;

            // Get to valid character in s
            while (i >= 0) {
                if (s[i] == '#') {
                    Sskip++;
                    i--;
                }
                else if (Sskip > 0) {
                    Sskip--;
                    i--;
                }
                else {
                    break;
                }
            }

            // Get to valid character in t
            while (j >= 0) {
                if (t[j] == '#') {
                    Tskip++;
                    j--;
                }
                else if (Tskip > 0) {
                    Tskip--;
                    j--;
                }
                else {
                    break;
                }
            }

            // One string has a valid character, other doesn't
            if (i >= 0 && j < 0)
                return false;

            if (i < 0 && j >= 0)
                return false;

            // Both have valid characters but they don't match
            if (i >= 0 && j >= 0 && s[i] != t[j])
                return false;

            // Move to the next characters
            i--;
            j--;
        }

        return true;
    }
};
```


TC:O(n) , SC: O(1) 
