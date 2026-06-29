# Symmetric Tree

[LeetCode](https://leetcode.com/problems/symmetric-tree/)


<img width="354" height="291" alt="image" src="https://github.com/user-attachments/assets/c753e34f-5711-445a-9dff-5a37857ee133" />

Input: root = [1,2,2,3,4,4,3]

Output: true

# Approach Recursive

<img width="782" height="455" alt="image" src="https://github.com/user-attachments/assets/075cd4a3-fd1d-48ed-855b-015588b36bc7" />

<br>

- Check if root is NULL, if yes then return True
- Call isSymHelper function, with arguments as (root->left,root->right)
- isSymHelper(TreeNode *leftTree, TreeNode *rightTree), imagine them as two separate trees
  - compare if anyone from them is NULL, return True if both are NULL, else false, as one is NULL only and other has some value
  - if leftTree's value is not equals to rightTree's value, then return false
  - Now compare symmetric, by recursively calling isSymHelper to compare {leftTree->left,rightTree->right} && {leftTree->right, rightTree->left}
 
<br>

```cpp
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        return root==NULL || isSymHelper(root->left,root->right);
    }
    bool isSymHelper(TreeNode *leftTree, TreeNode *rightTree){ // Two different trees 
        if(leftTree==NULL || rightTree==NULL) return leftTree==rightTree;
        if(leftTree->val != rightTree->val) return false; //checked current node
        return isSymHelper(leftTree->left,rightTree->right) && isSymHelper(leftTree->right,rightTree->left);
    }
};
```

Time Complexity: O(N) where N is the number of nodes in the Binary Tree. This complexity arises from visiting each node exactly once during the traversal and the function compares the nodes in a symmetric manner.

Space Complexity: O(1) as no additional data structures or memory is allocated.
