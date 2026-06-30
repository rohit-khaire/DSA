# Length of Last Word

[LeetCode](https://leetcode.com/problems/length-of-last-word/submissions/2051366993/)

# Approach

We work from last index, and get the length of last word using indexes;

```cpp
class Solution {
public:
    int lengthOfLastWord(string s) {
        if(s.empty()) return 0;
        int end =s.size()-1;
        while(s[end] == ' ') end--;
        int i=end;
        while(i>=0 && s[i]!=' ') i--;
        // return s.substr(i+1,end+1);
        return end-i;
    }
};
```

TC: AT worst O(N) & SC:O(1)
