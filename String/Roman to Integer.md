# Roman to Integer

[LeetCode](https://leetcode.com/problems/roman-to-integer/)

Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.

They are generally in decreasing order(Add to sum) and if order breaks then Subtract


| Symbol | Value |
| ------ | ----- |
| I      |     1 |
| V      |     5 |
| X      |    10 |
| L      |    50 |
| C      |   100 |
| D      |   500 |
| M      |  1000 |

### Subtractive Pairs to Remember

| Pair | Value |
| ---- | ----: |
| IV   |     4 |
| IX   |     9 |
| XL   |    40 |
| XC   |    90 |
| CD   |   400 |
| CM   |   900 |

In IV => I < V => V-I = 5 - 1 = 4

### Quick Trick

* If current symbol **< next symbol** → **Subtract**
* Otherwise → **Add**
* Always add last symbol


# Approach

- Traverse from left to right.
- If current value is smaller than next value → subtract it.
- Otherwise → add it.
- Last character is always added.
- Roman numerals are usually written in decreasing order. 87654321
- A smaller numeral before a larger numeral means subtraction (IV, IX, XL, XC, CD, CM).
- Every character contributes exactly once, either as +value or -value.

```cpp
class Solution {
public:
    int romanToInt(string s) {
        // Roman is written in Decreasing Order 765432
        // if s[i]<s[i+1] => Subtract and directly move to s[i+2]
        // If s[i]>s[i+1] => Addition
        int sum=0;
        unordered_map<char, int> mpp = {
            {'I', 1}, {'V', 5}, {'X', 10},
            {'L', 50}, {'C', 100}, {'D', 500}, {'M', 1000}
        };
        for(int i=0;i<s.size()-1;i++){  //Traverse while we have next element, as last element will be alone so can add it directly at last
            //there exists next element
            if(mpp[s[i]]<mpp[s[i+1]]){  //next ele is graeter, which breaks the order
                sum-=mpp[s[i]];
            }
            else{
                    sum+=mpp[s[i]];
            }
        }
        return sum+mpp[s.back()]; //always add last element
        
    }
};
```

O(n) time, O(1) space as there are only 7 entries in Map



