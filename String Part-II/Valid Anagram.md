# Valid Anagram

[LeetCode](https://leetcode.com/problems/valid-anagram/description/)

All the character in s are present in t ( same frequency of characters)

Input: s = "anagram", t = "nagaram"

Output: true

<img width="1559" height="1098" alt="image" src="https://github.com/user-attachments/assets/0196f5c1-3418-491e-b59b-2dcf1927f3c3" />


# Brute Approach using Sorting

Sort both the strings and match CHarcater by Character

- First, check if the lengths of both strings are equal. If not, they can't be anagrams and return false immediately.
- If the lengths match, sort both strings using a built-in sorting algorithm.
- Once sorted, iterate through each character of both strings and compare them one by one.
- If any character mismatch is found, return false.
- If all characters match, return true, confirming that the strings are anagrams.

TC=O(NlogN) for sorting string s + O(NlogN) for sorting string t + O(N) for string matching

SC=O(1)

# OPTIMAL using hashing(frequency of characters)

- First, check if the lengths of both strings are equal. If not, return false immediately as they cannot be anagrams.
- Initialize a frequency array of size 26 (for all lowercase English letters) and set all elements to 0.
- Traverse the first string and increment the frequency of each character.
- Traverse the second string and decrement the frequency of each character.
- At the same time check if all elements in the frequency array are zero. If any element is not zero (<0), return false as the characters do not match in frequency.
- If all frequencies are zero, the strings are anagrams and the function returns true.


```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        if(s.size()!=t.size()) return false;
        int freq[26]={0};
        for(int i=0;i<s.size();i++){
            freq[s[i]-'a']++;
        }
        for(int i=0;i<t.size();i++){
            freq[t[i]-'a']--;
            if(freq[t[i]-'a']<0) return false;
        }
        return true;
    }
};
```

TC=O(N) + O(N) for traversing both the strings to get count of characters

SC=O(26)=O(1)
