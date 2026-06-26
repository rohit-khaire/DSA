# Balanced Binary Tree

[LeetCode](https://leetcode.com/problems/balanced-binary-tree/)

Balanced BT => Left Height - Right Height = -1 or 0 or 1

Given a Binary Tree, return true if it is a Balanced Binary Tree else return false. A Binary Tree is balanced if, for all nodes in the tree, the difference between left and right subtree height is not more than 1..

# Approach using Recursion (DFS)

- If root is NULL, return 0
- get height of left subtree, if it's -1 means it's not balanced, without checking anything return -1
- get height of right subtree, if it's -1 means it's not balances, return -1
- get current node's height value, as abs(leftHeight-rightHeight)>1 , then return -1
- return max(leftHeight,rightHeight)+1, as from current node to parent node, distance is of +1

```cpp
class Solution {
public:
    int dfsHeight(TreeNode *root){
        if(root==NULL) return 0;
        int left = dfsHeight(root->left);
        if(left==-1) return -1;
        int right = dfsHeight(root->right);
        if(right==-1) return -1;
        if(abs(left-right)>1) return -1;
        return max(left,right)+1;
    }
    bool isBalanced(TreeNode* root) {
        return dfsHeight(root)!=-1;
    }
};
```

TC:O(N) and SC:(N) at worst if tree is skewed
