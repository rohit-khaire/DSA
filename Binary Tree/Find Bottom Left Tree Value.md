# Find Bottom Left Tree Value

[LeetCode](https://leetcode.com/problems/find-bottom-left-tree-value/description/)

Find the Last Row's (level's) most left Value

# Approach that beats 100%

Recursive:

- Get the Left View of Binary Tree
- return the Last element of Result Array

```cpp

class Solution {
public:
    void findLastLeft(TreeNode *root, int level, vector<int> &res){
        if(root==NULL) return;
        if(level==res.size()) res.push_back(root->val);
        findLastLeft(root->left,level+1,res);
        findLastLeft(root->right,level+1,res);
    }
    int findBottomLeftValue(TreeNode* root) {
        vector<int> res;
        findLastLeft(root,0,res);
        return res.back();
    }
};
```

**TC: O(N) and SC: O(H) where H=logN for balanced tree and H=N for skewed tree**
