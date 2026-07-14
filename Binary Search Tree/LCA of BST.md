# Lowest Common Ancestor of a Binary Search Tree

[LeetCode](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/description/)

# Approach - Recursive

- If p & q both are smaller than current root value, then just move to left.
- If p & q both are greater than current root value, then just move to right.
- When we get a Root where p and q gets different, A root where p and q both gets separated then that our Result(LCA)

<br>

```cpp
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root==NULL) return root;
        if(p->val < root->val && q->val < root->val){
             return lowestCommonAncestor(root->left,p,q);
        }else if(p->val > root->val && q->val > root->val){
            return lowestCommonAncestor(root->right,p,q);
        }
        return root;
    }
};
```

TC:O(H) & SC:O(H)
