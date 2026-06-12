# Inorder Traversal of Binary Tree

[LeetCode](https://leetcode.com/problems/binary-tree-inorder-traversal/)

## Solved in 1st Attempt without even thinking at 12:23 AM🕧

Left Node - root - Right Node 

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    void inorder(TreeNode *root, vector<int> &res){
        if(root==NULL){
            return;
        }
        inorder(root->left,res);
        res.push_back(root->val);
        inorder(root->right,res);
    }
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        inorder(root,res);
        return res;
    }
};
```

Complexity
- Time Complexity: O(N) (Every node is visited exactly once.)
- Auxiliary Space: O(H) (Recursion stack, where H = height of tree.)
- Worst Case Space: O(N) (skewed tree)
- Best/Average Space: O(log N) (balanced tree)
