# Path Sum

[Leetcode](https://leetcode.com/problems/path-sum/)

return is there any path with sum==targetSum, if yes return True, else False


# Approach - Recursive

- If root==NULL, return false
- if you are Leaf Node, check if targetSum==root->val, return True, else False
- check for rec(root->left,targetSum-root->val) pass targetSum as reduced/required, and for rec(root->right,targetSum-root->val), Perform it's or operation

```cpp
class Solution {
public:
    bool hasPathSum(TreeNode* root, int targetSum) {
        if(root==NULL) return false;
        if(root->left==NULL && root->right==NULL){
            return root->val==targetSum;
        }
        return hasPathSum(root->left,targetSum-root->val) || hasPathSum(root->right,targetSum-root->val);
    }
};
```

TC: O(N) & SC:O(H)
