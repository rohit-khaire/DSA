# Longest Common Prefix

[LeetCode](https://leetcode.com/problems/longest-common-prefix/)

Input: strs = ["flower","flow","flight"]

Output: "fl"

## OPTIMAL SOLUTION 1 - without sorting


Simple Explanation

* Take the **first string as the reference string**.
* Traverse each character of the reference string from left to right.
* For every character position `i`, check whether **all other strings** have:

  * a character at position `i` (string is long enough)
  * the same character as the reference string.
* If any string is shorter or has a different character, stop immediately.
* The characters checked successfully so far form the Longest Common Prefix.

### Example

```text
["car", "can", "care"]

Reference String = "car"
```

* Check position `0` → `'c'`

  * car[0] = c
  * can[0] = c
  * care[0] = c
  * ✅ Match

* Check position `1` → `'a'`

  * car[1] = a
  * can[1] = a
  * care[1] = a
  * ✅ Match

* Check position `2` → `'r'`

  * car[2] = r
  * can[2] = n ❌ Mismatch

Stop.

```cpp
return "ca";
```

or

```cpp
return strs[0].substr(0, 2);
```

---

## Pseudocode

```cpp
for each character i in first string
{
    for every other string
    {
        if string is too short
           OR character differs
              return prefix till i
    }
}

return first string
```

---

## Time Complexity

Let:

* `N` = number of strings
* `M` = length of the shortest/common prefix candidate

In the worst case:

```text
["flower","flower","flower"]
```

For every character position (`M` positions), we compare with all `N` strings.

So:

NxM

### Why?

```text
M positions
×
N string comparisons at each position
```

---

## Space Complexity

Only a few variables are used.

O(1)

If you count the returned string separately:

```cpp
return strs[0].substr(0, i);
```

then the returned string itself takes `O(M)` space, but auxiliary space remains:

O(1)

---


This is actually the **optimal solution** for LCP (often called *Vertical Scanning*), not merely a brute-force approach.

```cpp
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        if(strs.size()==0) return "";
        string refStr = strs[0];
        int i,j;
        for( i=0;i<refStr.size();i++){ //index
            for(j=1;j<strs.size();j++){ //all other strings
                if(i>=strs[j].size() || refStr[i]!=strs[j][i]){
                    return refStr.substr(0,i);
                }
            }
        }
        return refStr.substr(0,i);
    }
};
```

TC=O(M*N) where M is no. of characters in reference Str and N is No. of Strings, and SC=O(1)


## OPTIMAL using sort

Sort and just compare 1st and last strings

- The common prefix across all strings must exist between the smallest and largest string when sorted lexicographically.
- Sorting the array helps bring these boundary strings to the extremes.
- By comparing only the first and last strings, we can determine the full common prefix shared by the entire array.
- Character-wise comparison from the beginning allows us to identify where the prefix stops.
- The point at which the characters start differing marks the end of the shared prefix.
- The portion before this mismatch is the longest common prefix among all strings.

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
