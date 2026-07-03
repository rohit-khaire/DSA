# Search in BST

[LeetCode](https://leetcode.com/problems/search-in-a-binary-search-tree/)

Search the value in BST, bst is left<root<right

# Approach

- Point node to Root of BST
- while(node is not NULL)
  - check the value of node, if it's equals to value needed, we return this Node
  - move node to it's currect child, if required value is smaller, then go to left child.
- return NULL, as There is no node with required value

<br> 

```cpp
class Solution {
public:
    TreeNode* searchBST(TreeNode* root, int val) {
        if(root==NULL) return NULL;
        TreeNode *node = root;
        while(node){
            if(node->val==val) return node;
            node = (node->val>val)?node->left:node->right;
        }
        return NULL;
    }
};
```

- Time Complexity: O(log N),Each step eliminates half of the tree, just like binary search. However, in the worst case (unbalanced tree), it could be O(N).
- SC: O(1)
