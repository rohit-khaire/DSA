# Construct Binary Search Tree from Preorder Traversal

[LeetCode](https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/description/)

## Approach - Brute Force

- Iterate through whole array and create a Node and attach it to it's proper place in BST

## Approach - Recursive

- We have one global variable ``i`` to Traverse the Array of Preorder
- We only keep track of Upper bound, as for each node upper bound is important
- Pass array, global variable ia dn Upper bound as INT_MAX to function build, as for root, INT_MAX is bound
- build(list,i,upperBound)
  - if i==list.size() || , we return NULL
  - Create node with value of current list[i]
  - Increment the i, i++
  - Now for current root's left, call the build(list,i,node->val) as for left child, I am the Upperbound, left child cannot be greater than me
  - Now for current node's right call the build(list,i,upperBound) as for right child, my upperBound is it's upperBound, as Right child will be greater than me but smaller than my UpperBound
  - return root
 
- <br>


```cpp
class Solution {
public:
    TreeNode* bstFromPreorder(vector<int>& preorder) {
        int i=0;
        return build(preorder,i,INT_MAX);
    }
    TreeNode* build(vector<int> &list,int &i,int upperBound){
        if(i==list.size() || list[i]>upperBound) return NULL;
        TreeNode *node = new TreeNode(list[i]);
        i++;
        node->left = build(list,i,node->val);
        node->right = build(list,i,upperBound);
        return node;
    }
};
```

TC: O(3N)=O(N) as for each node we goto left & come back then goto rightchild and comeback, and SC=(1) as only recursive stack is used
