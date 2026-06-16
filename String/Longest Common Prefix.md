# Longest Common Prefix

[LeetCode](https://leetcode.com/problems/longest-common-prefix/)

## OPTIMAL using sort

Sort and just compare 1st and last strings

```cpp
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        if(strs.empty()) return "";
        sort(strs.begin(),strs.end());
        int i;
        int len = min(strs[0].size(), strs.back().size());
        for(i=0;i<len;i++){
            if(strs[0][i]!= strs[strs.size()-1][i]){
                break;
            }
        }
        return strs[0].substr(0,i);
        
    }
};
```

TC= O(NlogN×M) as sorting the strings may lead to scanning all the characters of String +O(M) for 1st and Last strings comparison

Sc=O(1)
