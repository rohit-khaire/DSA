# Morris Preorder Traversal of a Binary Tree

[LeetCode](https://leetcode.com/problems/binary-tree-preorder-traversal/)


Similar as Morris Inorder, same thinking

Just apply it on:

<img width="177" height="105" alt="image" src="https://github.com/user-attachments/assets/b57e973b-4f12-472d-bfd1-e91c300c37b3" />

and on

<img width="483" height="462" alt="image" src="https://github.com/user-attachments/assets/0e89a556-b4c5-46bf-acee-b8c8a8c05e77" />

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
    vector<int> preorderTraversal(TreeNode* root) {
        //Morris Preorder with TC:O(N) and SC:O(1)
        vector<int> res;
        if(root==NULL) return res;
        TreeNode *cur=root;
        while(cur!=NULL){
            if(cur->left==NULL){  //Imagine red wala 1st image with left child NULL
                res.push_back(cur->val);
                cur=cur->right;
            }else{
                // I have left subtree
                TreeNode *prev=cur->left; //check is there linking to predecessor
                while(prev->right!=NULL && prev->right!=cur){
                    prev=prev->right;
                }
                if(prev->right==NULL){ //No thread(link)
                    prev->right=cur;
                    res.push_back(cur->val);
                    cur=cur->left;
                }else{
                    //already linked to cur (There is thread)
                    prev->right=NULL;
                    cur=cur->right;
                }
            }
        }
        return res;


    }
};
```

**TC: O(N) and SC:O(1)**
