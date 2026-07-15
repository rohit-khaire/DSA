# BST Iterator

[LeetCode](https://leetcode.com/problems/binary-search-tree-iterator/)

``next()`` function returns the in-order next of current node, this is called only when there is next In-order Node

``hasNext`` function return True if there is next In-order Node

``BSTIterator(TreeNode* root)`` initializes as Root of BST


# Brute Approach - Using Array

Perform in-order traversal of BST and store the node's values in an Array

Now result becomes easy, initialize next to -1, if next+1 exists then return hasNext returns True

TC:O(1) for next function

**SC:O(N)**

# Approach - Using Stack (Iterative)

- When BSTIterator is initialized, store it and all the elements to it's left in Stack
- When Next is called, just get the top and store it as node, and pop it, if node has right, then Apply same BSTIterator constructor on node->right (store it and it's left all elements)
- Return node->val
- hasNext returns true when stack is not empty, when stack is empty it returns false

```cpp
class BSTIterator {
    stack<TreeNode*> st;
public:
    BSTIterator(TreeNode* root) {
        while(root){
            st.push(root);
            root=root->left;
        }
    }
    
    int next() {
        TreeNode *node = st.top();
        st.pop();
        if(node->right){
            TreeNode * rig = node->right;
            while(rig){
                st.push(rig);
                rig=rig->left;
            }
        }
        return node->val;
    }
    
    bool hasNext() {
        return !st.empty();
    }
};

/**
 * Your BSTIterator object will be instantiated and called as such:
 * BSTIterator* obj = new BSTIterator(root);
 * int param_1 = obj->next();
 * bool param_2 = obj->hasNext();
 */
```

TC:O(1) for next function

**SC:O(1)**

