# Invert Binary Tree

[Leetcode](https://leetcode.com/problems/invert-binary-tree/)

Given an Binary Tree, invert it by making left child as right and right child as left

<img width="761" height="182" alt="image" src="https://github.com/user-attachments/assets/6f594a44-c2d1-483b-aad3-e8d89552d326" />

<br>

# Approach - Recursion 

For Each Node

- If current root is NULL, return it
- Swap its left and right children.
- Recursively invert the left subtree.
- Recursively invert the right subtree.
- return root

**Code:**

```cpp
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if(root==NULL) return root;
        swap(root->left,root->right);
        invertTree(root->left);
        invertTree(root->right);
        return root;
    }
};
```

TC:O(N) and SC:O(H)
