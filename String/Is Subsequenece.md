# Is Subsequence

[Leetcode](https://leetcode.com/problems/is-subsequence/)

Given two strings s and t, return true if s is a subsequence of t, or false otherwise.

A subsequence of a string is a new string that is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. 

(i.e., "ace" is a subsequence of "abcde" while "aec" is not).


Input: s = "abc", t = "ahbgdc"

Output: true

Input: s = "axc", t = "ahbgdc"

Output: false

# Approach - Two pointers

- We have 2 strings s and t
- point i to s and j to t
- we keep moving while(i<sn && j<tn)
  - If s[i]==t[j], we move i ahead
  - Move j++
- if our i is pointing to s.size()+1, we then return true
- else false


 **Code:**


```cpp
class Solution {
public:
    bool isSubsequence(string s, string t) {
        int sn = s.size();
        int tn = t.size();
        int i=0,j=0;
        while(i<sn && j<tn){
            if(s[i]==t[j]){
                i++;
            }
            j++;
        }
        return (i==sn)? true: false;
    }
};
```



TC:O(t.size() or tn) and SC:O(1)
