# Preoder Traversal

[LeetCode](https://leetcode.com/problems/binary-tree-preorder-traversal/)

Root - Left - Right

# Using Stack (Iterative) (Without Recursion)

- We point our node to root, have stack<TreeNode*> and result vector
- If root is NULL, return empty vector as it is
- Infinite Loop (We will break it later when our stack is empty and node is NULL)
  - If current node is NOT NULL
    - print it (add to result vector)
    - Add this Node to Stack
  - Else current node is NULL (reached left end)
    - If stack is empty, then return the Result
    - pop TreeNode from Stack and go to it's right


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
        vector<int> res;
        if(root==NULL) return res;
        stack<TreeNode*> s;
        TreeNode *node = root;
        while(1){
            if(node!=NULL){
                s.push(node);
                res.push_back(node->val);
                node=node->left;
            }else{
                if(s.empty()) return res;
                node = s.top();
                s.pop();
                node=node->right;
            }
        }
    }
};
```


- Time Complexity : O(N)
- Space Comp: O(H) (H = height of tree)
- SC when Balanced Tree: O(log N)
- SC when Skewed Tree: O(N) , as stack will store all the nodes


# Using Recursion

- Have base case as return if root is NULL
- print root
- preorder(root->left)
- preorder(root->right)

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
    void preorder(TreeNode *root, vector<int> &res){
        if(root==NULL) return;
        res.push_back(root->val);
        preorder(root->left, res);
        preorder(root->right,res);
    }
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> res;
        preorder(root,res);
        return res;
    }
};
```

- Time Complexity: O(N)
- Space Complexity: O(H)
    - Balanced Tree → O(log N)
    - Skewed Tree → O(N)
