# Level Order Traversal

[LeetCode](https://leetcode.com/problems/binary-tree-level-order-traversal/)

BFS on Binary Tree

# Approach

Use one Queue to store the Nodes


- Have one Queue ro store the Nodes
- Push root node in Queue
- loop while Queue is not empty
  - Get the No. of Nodes in Current Level (get the size of queue)
  - Loop for each node in current level
    - check if it has left, if yes then push it in Queue
    - check if it has right, if yes then push it in Queue
    - push current node in level vector (node->val)
    - pop the node from queue
  - Push level in result vector

```cpp
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        if(root==NULL) return res;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty()){
            int n = q.size();
            vector<int> level;
            for(int i=0;i<n;i++){ //For nodes in that level
                TreeNode *node = q.front();
                q.pop();
                level.push_back(node->val);
                if(node->left) q.push(node->left);
                if(node->right) q.push(node->right);
            }
            res.push_back(level);
        }
        return res;
    }
};
```

TC: O(N) and SC: O(Max width of Tree) of complete BT SC:O(N/2) and in worst case SC:O(N)
