# Flatten BT to LL

[LeetCode](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/)

<img width="1021" height="461" alt="image" src="https://github.com/user-attachments/assets/48e48237-e96b-449d-b82f-e8b7642693fe" />


# Approach : Recursion

Use prev=NULL,

We start from very last of preorder, very right node of root, and keep linking and goes upwards.

- We point prev to NULL
- Take root in flatten(root) recursion function
- if root is NULL, we return;
- apply rec func: flatten(root->right) // We can go to last node of preorder
- apply rec func: flatten(root->left)
- Imagine we are at very last node of preorder, most right last
- We make root->right=prev & root->left=NULL;
- make prev point root


```cpp
class Solution {
public:
    TreeNode *prev=NULL;
    void flatten(TreeNode* root) {
        if(root==NULL) return;
        flatten(root->right);
        flatten(root->left);
        root->right=prev;
        root->left=NULL;
        prev=root;
    }
};
```

TC: O(N) & SC:O(H) = O(N) at worst


# Apprach : Using Single Stack

- Use a stack to keep Track of Nodes
- Push the Root to the Stack
- Loop, while(!st.empty())
  - get st.top() as node and pop it
  - now, if node has right, then push it. **Push right first as we will be connecting right nodes at last**
  - now, if node has left, then push it.
  - if stack is not empty, then stack's top is current node's left
  - so make current node's left as NULL and node's right as stack's top

```cpp
class Solution {
public:
    void flatten(TreeNode* root) {
        if(!root) return;
        stack<TreeNode*> st;
        st.push(root);
        while(!st.empty()){
            TreeNode *node = st.top();
            st.pop();
            if(node->right) st.push(node->right); // as right is to be linked at last
            if(node->left) st.push(node->left);
            if(!st.empty()) node->right=st.top();
            node->left=NULL;
        }
    }
};
```

TC: O(N) and SC:O(H) = O(N)


# Approach : Morris Preorder

**Using Threaded Tree** concept

- point cur to root
- loop while(cur)
  - if(cur->left)
    - make prev = cur->left
    - go to most right node of prev using loop
    - make prev->right = cur->right
    - now we can make cur->right = cur->left and make cur->left = NULL
  - now we can move to cur->right

```cpp
class Solution {
public:
    void flatten(TreeNode* root) {
        if(root==NULL) return;
        TreeNode *cur = root;
        while(cur){
            if(cur->left){
                TreeNode *prev = cur->left;
                while(prev->right) prev=prev->right;
                prev->right = cur->right;
                cur->right=cur->left;
                cur->left = NULL;
            }
            cur=cur->right;
        }
    }
};
```


TC: O(N) and SC:O(1)
