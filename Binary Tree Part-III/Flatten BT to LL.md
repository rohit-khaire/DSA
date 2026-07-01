# Flatten BT to LL

[LeetCode](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/)

<img width="1021" height="461" alt="image" src="https://github.com/user-attachments/assets/48e48237-e96b-449d-b82f-e8b7642693fe" />


# Approach : Recursion

Use prev=NULL,

We start from very last of preorder, very right node of root, and keep linking and goes upwards.

- We point prev to NULL
- Take root in flatten(root) recursion function
- if root is NULL, we return;
- apply rec func: flatten(root->right) // We can go to last node of preorder
- apply rec func: flatten(root->left)
- Imagine we are at very last node of preorder, most right last
- We make root->right=prev & root->left=NULL;
- make prev point root


```cpp
class Solution {
public:
    TreeNode *prev=NULL;
    void flatten(TreeNode* root) {
        if(root==NULL) return;
        flatten(root->right);
        flatten(root->left);
        root->right=prev;
        root->left=NULL;
        prev=root;
    }
};
```

TC: O(N) & SC:O(H) = O(N) at worst
