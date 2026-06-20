# Inorder Traversal of Binary Tree

[LeetCode](https://leetcode.com/problems/binary-tree-inorder-traversal/)

## Solved in 1st Attempt without even thinking at 12:23 AM🕧 (Recursion)

Left Node - root - Right Node 

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
    void inorder(TreeNode *root, vector<int> &res){
        if(root==NULL){
            return;
        }
        inorder(root->left,res);
        res.push_back(root->val);
        inorder(root->right,res);
    }
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        inorder(root,res);
        return res;
    }
};
```

Complexity
- Time Complexity: O(N) (Every node is visited exactly once.)
- Auxiliary Space: O(H) (Recursion stack, where H = height of tree.)
- Worst Case Space: O(N) (skewed tree)
- Best/Average Space: O(log N) (balanced tree)


# Inoder using Stack (Iterative)

- Initialize an empty stack and point the current node to the root of the binary tree.
- Enter a loop that continues as long as there are nodes in the stack or the current node is not null. Or else have infinite loop that breaks when stack is empty and current node is NULL.
- If the current node is not null, push it onto the stack and move to its left child. Continue this process until a node with no left child is reached. (node reaches NULL, this will be left most NULL)
- Once a null node is encountered, pop the top node from the stack, process it (e.g., add its value to the result array), and move to its right child.
- Repeat this process of pushing and popping nodes, alternating between moving left and right, until the stack is empty and the current node is null.
- At the end of the process, return the result array, which will contain the inorder traversal of the binary tree.

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
    void inorder(TreeNode *root, vector<int> &res){
        if(root==NULL){
            return;
        }
        TreeNode *node = root;
        stack<TreeNode*> s;
        while(1){
            if(node!=NULL){
                s.push(node);
                node=node->left;
            }
            else{
                if(s.empty()) break;
                node = s.top();
                s.pop();
                res.push_back(node->val);
                node=node->right;
            }
        }
    }
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        inorder(root,res);
        return res;
    }
};
```

Time Complexity: O(n), where n is the number of nodes in the binary tree. Each node is visited exactly once.

Space Complexity: O(h), where h is the height of the binary tree. This is the space required for the stack to store the nodes during traversal + O(n) to store the result array


In Skewed tree → SC: O(N) for stack, this is worst case


