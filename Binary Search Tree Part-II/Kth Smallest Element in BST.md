# Kth Smallest Element in BST

[LeetCode](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

# Approach - Recursion inorder

BST's inorder = sorted form

Keep track of current node using counter, and when cnt==k, return


```cpp
class Solution {
public:
    int kthSmallest(TreeNode* root, int k) {
        int cnt=0;
        int ans=0;
        inorder(root,k,cnt,ans);
        return ans;
    }
    void inorder(TreeNode *root,int k,int &cnt,int &ans){
        if(root==NULL) return;
        inorder(root->left,k,cnt,ans);
        cnt++;
        if(cnt==k){
            ans=root->val;
            return;
        }
        inorder(root->right,k,cnt,ans);
    }
};
```

TC: O(N) and SC:O(H)
