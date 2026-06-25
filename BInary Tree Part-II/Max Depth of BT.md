# Max Depth of BT

[LeetCode](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/)

Height of Binary Tree

Given the root of a Binary Tree, return the height of the tree. The height of the tree is equal to the number of nodes on the longest path from root to a leaf.

# Approach using Recursion

This approach is like go from Top to Bottom and start returning from Bottom to Top.

- If root is NULL, then return 0, as height is zero
- find height of left subtree, by recusrive call to root->left
- find height of right subtree, by recusrive call to root->right
- maximum height from the current node to leaf is max(left,right)+1
- return max(left,right)+1

```cpp
class Solution {
public:
    int findDepth(TreeNode *root, int &maxi){
        if(root==NULL) return 0;
        int left = findDepth(root->left,maxi);
        int right = findDepth(root->right,maxi);
        maxi = max(maxi,max(left,right)+1);
        return max(left,right)+1;
    }
    int maxDepth(TreeNode* root) {
        int maxi=0;
        findDepth(root,maxi);
        return maxi;
    }
};
```

# Approach using BFS

Just count Number of Levels in Binary Tree

```cpp
class Solution {
public:
    void bfs(TreeNode *root, int &level){
        if(root==NULL) return;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty()){
            int n=q.size();
            for(int i=0;i<n;i++){
                TreeNode *node = q.front();
                if(node->left) q.push(node->left);
                if(node->right) q.push(node->right);
                q.pop();
            }
            level++;
        }
    }
    int maxDepth(TreeNode* root) {
        int level=0;
        bfs(root,level);
        return level;
    }
};
```
