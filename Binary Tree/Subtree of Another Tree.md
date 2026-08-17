# Subtree of Another Tree

[Leetcode](https://leetcode.com/problems/subtree-of-another-tree/)

Given two roots of 2 Binary Trees

Return True if right subtress exists in left Tree

<img width="532" height="400" alt="image" src="https://github.com/user-attachments/assets/ec1e89fa-4b1c-47de-8bc8-8b5852e44b5d" />


# Approach - Recursive

**isSubtree(root,subRoot):** Checks if right subtree's root is matching with left tree's root(Current Node) 

- if subRoot is NULL, return True; as Null can be found in left tree
- if left tree's root is NULL, return false; as in NULL Tree we cannot find subRoot
- call helper function, isSame(root,subRoot); checks if both trees are same or not; if same, return True
- return isSubtree(root->left,subRoot) || isSubtree(root->right,subRoot); Check for root's left subtree and root's right subtree


<br>

**isSame(root1,root2):** Checks if both tree are identical or not

- if both roots are NULL, return true;
- if anyone from them is NULL then return false, as trees aren't identical
- if both root's values doesn't matches, return False;
- check the same for isSame(root1->left,root2->left) && isSame(root1->right,root2->right);

```cpp
class Solution {
public:
    bool isSame(TreeNode *root1, TreeNode *root2){
        if(root1==NULL && root2==NULL) return true;
        if(root1==NULL || root2==NULL) return false; //only one of them is NULL
        if(root1->val != root2->val) return false;
        return isSame(root1->left,root2->left) && isSame(root1->right,root2->right);
    }
    bool isSubtree(TreeNode* root, TreeNode* subRoot) {
        if(subRoot==NULL) return true;
        if(root==NULL) return false;
        if(isSame(root,subRoot)) return true; //At current node as root, can our both trees be same
        return isSubtree(root->left,subRoot) || isSubtree(root->right,subRoot);

    }
};
```

