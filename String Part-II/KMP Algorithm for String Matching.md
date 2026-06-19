# KMP



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


# Algorithm for Construction of LPS Array

lps[0] is always 0 since a string of length one has no non-empty proper prefix. We store the value of the previous LPS in a variable len, initialized to 0. As we traverse the pattern, we **compare the current character at index i, with the character at index len.**

Case 1 - pat[i] == pat[len]: this means that we can simply extend the LPS at the previous index, so increment len by 1 and store its value at lps[i].

Case 2 - pat[i] != pat[len] and len == 0: it means that there were no matching characters earlier and the current characters are also not matching, so lps[i] = 0.

Case 3 - pat[i] != pat[len] and len > 0: it means that we can't extend the LPS at index i-1. However, there may be a smaller prefix that matches the suffix ending at i. To find this, we look for a smaller suffix of pat[i-len...i-1] that is also a proper prefix of pat. We then attempt to match pat[i] with the next character of this prefix. If there is a match, pat[i] = length of that matching prefix. Since lps[i-1] equals len, we know that pat[0...len-1] is the same as pat[i-len...i-1]. Thus, rather than searching through pat[i-len...i-1], we can use lps[len - 1] to update len, since that part of the pattern has already been matched. 






