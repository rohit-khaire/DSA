# Check if two trees are identical or not

[LeetCode](https://leetcode.com/problems/same-tree/)

Given two Binary Trees, return true if the two trees are identical, otherwise return false..

Two trees are said to be identical if these three conditions are met for every pair of nodes :
- Value of a node in the first tree is equal to the value of the corresponding node in the second tree.
- Left subtree of this node is identical to the left subtree of the corresponding node.
- Right subtree of this node is identical to the right subtree of the corresponding node.

# Approach using DFS Recursion
Using DFS Recursion to travers, you can use any traversal method,

Just compare the current node and repeat/recursive call to root's left and for root's right

```cpp
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if(p==NULL && q==NULL) return true; // Case 1: If both nodes are NULL, they are identical
        if(p==NULL || q==NULL) return false; //// Case 2: If only one of the nodes is NULL, they are not identical
        //Above 2 lines can be written as : if(p==NULL || q==NULL) return p==q
        return (p->val==q->val) && isSameTree(p->left,q->left) && isSameTree(p->right,q->right);
    }
};
```

TC: O(N) and SC:O(N) in worst case when skewed Tree
