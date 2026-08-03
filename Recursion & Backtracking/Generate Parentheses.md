# Generate Parentheses


[Leetcode](https://leetcode.com/problems/generate-parentheses/)


Given Integer N, This is Maximum Number of Parentheses you can have. Create all possible combinations of N Parentheses:

Like for N=2, we can have ["(())","()()"]

Just provide all possible combinations of N open brackets '('

# Approach - Recursive & backtracking


- Start with an empty string.
- Keep track of:
  - open = number of '(' used.
  - close = number of ')' used.
- If open < n, recursively add '('. Then remove it.
- If close < open, recursively add ')'. Then remove it.
- Base Case:
  - When the string length becomes 2*n, store it in the answer. As current string is one of possible combinations of N '('
  - Or else this base case also works: Instead of 2*n length, we can also stop when open==n && close==n


```cpp
class Solution {
public:
    void rec(string &str,int open,int close,int n,vector<string> &ans){
        //Base case
        // if(str.size() == n*2){ //2*N is max length possible with N opening brackets
        if(open==n && close==n){
            ans.push_back(str);
            return;
        }
        if(open<n){
            str.push_back('(');
            rec(str,open+1,close,n,ans);
            str.pop_back();
        }
        if(close<open){
            str.push_back(')');
            rec(str,open,close+1,n,ans);
            str.pop_back();
        }
    }
    vector<string> generateParenthesis(int n) {
        vector<string> ans;
        string str;
        rec(str,0,0,n,ans);
        return ans;
    }
};
```


