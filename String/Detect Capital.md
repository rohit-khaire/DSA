# Detect Capital

[LeetCode](https://leetcode.com/problems/detect-capital/submissions/2053656165/)

All small case or All Uppercase or only 1st letter is Uppercase

```cpp
class Solution {
public:
    bool detectCapitalUse(string word) {
        int upper=0;
        for(int i=0;i<word.size();i++){
            if(isupper(word[i])) upper++;
        }
        return upper==0 || upper==word.size() || (upper==1 && isupper(word[0])); 
    }
};
```

TC: O(N) and SC: O(1)
