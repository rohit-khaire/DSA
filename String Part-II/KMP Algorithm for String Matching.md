# KMP

[LeetCode](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/)


Actually it's simple. **It gives 0ms on Burte Force (Naive String Matching) and gives 2 ms on KMP Solution**

We maintain a extra LPS array for pattern matching, which is preprocessed Pattern.

## Very Simple, Coded in 1st attempt by just understanding the Approach

# Algorithm

The basic idea behind KMP’s algorithm is: whenever we detect a mismatch (after some matches), we already know some of the characters in the text of the next window. We will take advantage of this information to avoid matching the characters that we know will anyway match. 

Matching Overview/Example:

txt = "AAAAABAAABA" 

pat = "AAAA"

We compare first window of txt with pat
<br><br>
txt = "**AAAA**ABAAABA" 

pat = "AAAA"  [Initial position]

We find a match. This is same as Naive String Matching.
<br><br>
In the next step, we compare next window of txt with pat.

txt = "A**AAAA**BAAABA" 
pat =  "AAAA" [Pattern shifted one position]

This is where KMP does optimization over Naive. In this second window, we only compare fourth A of pattern with fourth character of current window of text to decide whether current window matches or not. Since we know  first three characters will anyway match, we skipped matching first three characters.

<br>

**We pre-process pattern and prepare an integer array lps[] that tells us the count of characters to be skipped**


## In KMP Algorithm

- We preprocess the pattern and build LPS[] array for it. The size of this array is same as pattern length.
- **LPS** is the **Longest Proper Prefix** which is also a Suffix. A proper prefix is a prefix that doesn't include whole string.
  - For example, prefixes of "abc" are "", "a", "ab" and "abc" but proper prefixes are "", "a" and "ab" only. Suffixes of the string are "", "c", "bc", and "abc".
- Each value, lps[i] is the length of longest proper prefix of pat[0..i] which is also a suffix of pat[0..i].

``lps[i] = the longest proper prefix of pat[0..i] which is also a suffix of pat[0..i]. ``


# Construction of LPS Array

lps[0] is always 0 since a string of length one has no non-empty proper prefix. We store the value of the previous LPS in a variable len, initialized to 0. As we traverse the pattern, we **compare the current character at index i, with the character at index len.**

Case 1 - pat[i] == pat[len]: this means that we can simply extend the LPS at the previous index, so increment len by 1 and store its value at lps[i].

Case 2 - pat[i] != pat[len] and len == 0: it means that there were no matching characters earlier and the current characters are also not matching, so lps[i] = 0.

Case 3 - pat[i] != pat[len] and len > 0: it means that we can't extend the LPS at index i-1. However, there may be a smaller prefix that matches the suffix ending at i. To find this, we look for a smaller suffix of pat[i-len...i-1] that is also a proper prefix of pat. We then attempt to match pat[i] with the next character of this prefix. If there is a match, pat[i] = length of that matching prefix. Since lps[i-1] equals len, we know that pat[0...len-1] is the same as pat[i-len...i-1]. Thus, rather than searching through pat[i-len...i-1], we can use lps[len - 1] to update len, since that part of the pattern has already been matched. 


# Algo for Construction of LPS Array

- Take Pattern as input
- Have LPS array with same size as of input Pattern Array, make LPS[0]=0, as it's always 0
- get Pattern Length (m), so that we can traverse the whole pattern to build LPS Array
- we point len or j to 0th index and, i to 1st index (j=0 and i=1)
- we start traversing pattern using i and build LPS at each ith index, while(i<m)
  - if current character (pattern[i]) is == pattern[j] (character at j) (BOTH chars match)
    - Store the lenghth from 0 to j index at lps[i] (lps[i]=j+1) (If on next character, a missmatch occurs, then we can just move to this index)
    - Move j and i ahead (j++ and i++)
  - Else there is a Mismatch (pattern[i]!=pattern[j])
    - if j==0 (No matching prefix found)
      - lps[i] = 0;
      - Move i ahead (i++)
    - if j!=0 (There is matching prefix)
      - Move j to previous index's val of lps (j=LPS[j-1])
      - Stay at same position ( i remains as it is, don't change it's position )
- return LPS Array


# Algo for Searching Pattern in Text using LPS

We traverse text only once, no backing, just start from 0 and no stop or reverse till end

- have i and j pointing 0th index, i will traverse Text and j will traverse Pattern
- Now start matching the corresponding characters:
- if j==pattern.size, then we found full pattern at i-j index and now move j to LPS[j-1] 
- if Matched (text[i]==pattern[j]), move both ahead (i++ and j++)
- if NoMatch (text[i]!=pattern[j]):
  - if j==0, then just move the text pointer (i++)
  - if j!=0, just point j to LPS[j-1]


```cpp
class Solution {
public:
    vector<int> buildLPS(string pattern){
        int m = pattern.size();
        vector<int> LPS(m,0);
        int j=0,i=1;
        while(i<m){
            if(pattern[i]==pattern[j]){
                LPS[i]=j+1;
                j++;
                i++;
            }else{
                if(j==0){
                    LPS[i]=0;
                    i++;
                }else{
                    //mismatch and prefix is present
                    j=LPS[j-1];
                }
            }
        }
        return LPS;
    }
    int strStr(string text, string pattern) {
        if(pattern=="") return 0;
        vector<int> LPS=buildLPS(pattern);
        int i=0,j=0;
        while(i<text.size()){
            if(j==pattern.size()) break;
            if(text[i]==pattern[j]){
                //character match
                i++;
                j++;
            }else{
                //no character match
                if(j==0){
                    i++;
                }else{
                    //there is prefix
                    j=LPS[j-1];
                }
            }
        }
        return j==pattern.size()?i-j:-1;  //if true, means pattern was found and hence loop was break
    }
};
```

<br>


| Step      | TC         | SC       |
| --------- | ---------- | -------- |
| Build LPS | O(M)       | O(M)     |
| Search    | O(N)       | O(1)     |
| Total     | **O(N+M)** | **O(M)** |




<br><br>

| Algorithm   | Best TC | Average TC | Worst TC | SC   |
| ----------- | ------- | ---------- | -------- | ---- |
| Brute Force | O(N)    | O(NM)      | O(NM)    | O(1) |
| Rabin-Karp  | O(N+M)  | O(N+M)     | O(NM)    | O(1) |
| KMP         | O(N+M)  | O(N+M)     | O(N+M)   | O(M) |




