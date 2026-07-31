# Merge Two Binary Trees

[Leetcode](https://leetcode.com/problems/merge-two-binary-trees/description/)

[YT Hello Byte Visualization Shorts](https://youtube.com/shorts/So4ZBzdyL3I?si=-RWEo0hDJFz9BB-Z)

<br>

<img width="1112" height="302" alt="image" src="https://github.com/user-attachments/assets/a9143271-49ce-41e9-848a-dcff4bf3d228" />


Given 2 Binary Trees, Return root of Binary Tree in which each node is left tree's node at that position + right tree's node at that position

# Approach : Recursion

<img width="324" height="320" alt="image" src="https://github.com/user-attachments/assets/50de64ab-c7d5-46df-8957-ae357c41b9e8" />


Given 2 roots of 2 different Trees

- If root1 is NULL, return root2 (As if root2 is also NULL, then NULL is returned as both trees are having NULL at that poistion. But if tree2 has node, then return it as then left tree's node will be considered as 0, which gives answer as 0+right tree's node's val)
- if root2 is NULL, then return root1
- root1->val += root2->val
- Now recursively call the function with root1->left and root2->left
- Now recursively call the function with root1->right,root2->right
- return root1 as Root Node

```cpp
class Solution {
public:
    TreeNode* mergeTrees(TreeNode* root1, TreeNode* root2) {
        if(root1==NULL) return root2;
        if(root2==NULL) return root1;
        root1->val += root2->val;
        root1->left = mergeTrees(root1->left,root2->left);
        root1->right = mergeTrees(root1->right,root2->right);
        return root1;
    }
};
```

TC:O(N) and SC:O(H)


# Can also perform same using BFS Iterative
