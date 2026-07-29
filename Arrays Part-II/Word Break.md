# Word Break

[LeetCode](https://leetcode.com/problems/word-break/)

# Approach 

## Algorithm (Word Break - DP)

1. Store all dictionary words in an **unordered set** for **O(1)** lookup.
2. Find the **maximum word length** (`maxLen`) in the dictionary. We find **`maxLen`** so that we **only check possible last-word lengths that can actually exist in the dictionary, avoiding unnecessary substring checks and improving efficiency.** So that we don't search for word greater than this size.
3. Create a boolean DP array of size `n + 1`, where:

   * `dp[i] = true` means the first `i` characters of the string can be segmented into dictionary words.
  
4. Initialize:

   * `dp[0] = true` (empty string is always valid).
5. For every prefix ending at position `i` (from `1` to `n`):

   * Try every possible **last word length** `len` from `1` to `min(maxLen, i)`. Hence we run loop from len=1 to min(maxLenand,i)
   * Let the last word be `s.substr(i - len, len)`. I is further and len moves from 1 to min(i,maxLen)
   * If:

     * `dp[i - len] == true` (the prefix before the last word is already breakable), **and**
     * the last word exists in the dictionary,
     * then set `dp[i] = true` and stop checking further lengths for this `i`.
6. After processing all positions, return `dp[n]`.

---

### Pseudocode

```text
Insert all dictionary words into a hash set.

Find maxLen = maximum length of any word.

Create dp[0...n] and initialize all to false.
dp[0] = true.

For i = 1 to n:
    For len = 1 to min(maxLen, i):

        If dp[i - len] is true AND
           substring(i - len, len) exists in dictionary:

            dp[i] = true
            Break

Return dp[n].
```

### Core Intuition

At every position `i`, ask:

> **"Can I make the first `i` characters by taking one valid dictionary word at the end and attaching it to an already valid prefix?"**

If the answer is **yes** for any possible last word, then `dp[i] = true`. This is the key idea behind the algorithm.

# Code

```cpp
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {

        unordered_set<string> dict(wordDict.begin(), wordDict.end());

        int n = s.size();

        int maxLen = 0;
        for (auto &word : wordDict)
            maxLen = max(maxLen, (int)word.size());

        vector<bool> dp(n + 1, false);
        dp[0] = true;

        for (int i = 1; i <= n; i++) {

            for (int len = 1; len <= maxLen && len <= i; len++) {

                if (dp[i - len] &&
                    dict.count(s.substr(i - len, len))) {

                    dp[i] = true;
                    break;
                }
            }
        }

        return dp[n];
    }
};
```
