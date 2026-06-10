# Valid Parentheses

[LeetCode](https://leetcode.com/problems/valid-parentheses/)

# OPTIMAL

- Whenever we get the opening bracket we will push it into the stack. I.e ‘{‘, ’[’, ’(‘.
- Whenever we get the closing bracket we will check if the stack is non-empty or not.
- If the stack is empty we will return false, else if it is nonempty then we will check if the topmost element of the stack is the opposite pair of the closing bracket or not.
- If it is not the opposite pair of the closing bracket then return false, else move ahead.
- After we move out of the string the stack has to be empty if it is non-empty then return it as invalid else it is a valid string.

```cpp
class Solution {
public:
    bool isValid(string s) {
        stack<char> st;
        for(auto it: s){
            if(it=='(' || it=='[' || it=='{'){
                st.push(it);
            }
            else{
                if(st.empty()) return false;
                if((it==')' && st.top()=='(') || (it==']' && st.top()=='[') || (it=='}' && st.top()=='{')){
                    st.pop();
                }else{
                    return false;
                }
            }
        } 
        return st.empty();
    }
};
```

**TC=O(N) and SC=O(N)**
