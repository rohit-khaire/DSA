# Zig Zag or Spiral Traversal

[LeetCode](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/submissions/2048652570/)

You just need to traverse level wise (BFS), but only change is first you go from left to right in level 0, then on level 2 you go from right to left. Then on Level 3 you from left to right.

You traverse in Zig Zag order.


# Approach

<img width="568" height="600" alt="image" src="https://github.com/user-attachments/assets/d7d60838-42c7-452c-af45-3acfa5591409" />


Use BFS and have a vector to store level, just store the current node on it's current index. Keep track of left or right by having one Boolean variable for it.


- Have a vector<vector<int>> to store levels. (result)
- Have a queue for BFS Traversal
- Push the Root in Queue
- Have boolean variable to keep track of direction, LeftToRight = True means need to travel from left to right
- Loop while Q is not Empty
  - get the no. of nodes in current level (q.size()) (n)
  - Have a Vector to store current Level (Have same size as of current level (n)), We will be storing current level using index and LeftToRight Variable's value
  - For each node in current Level
    - get the Queue's Front, and pop it
    - if it has left child, then push that child in Queue
    - If it has right child, then push that child in Queue
    - Get the Proper Index for current Node, If LeftToRight is True then it means store it on ith index in vector levevl, but if LeftToRight is False, then it means current level must be stored in reverse order so current node's index will be n-1-i
    - Store current node Value on Above Index in Vector Level
  - Push Current level in Result Vector
  - Make LeftToRight opposite, if it was True, then make it False, if it was False then make it True
 
<br> 

```cpp
class Solution {
public:
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        vector<vector<int>> res;
        if(!root) return res;
        queue<TreeNode*> q;
        q.push(root);
        bool LeftToRight=true;
        while(!q.empty()){
            int n = q.size(); //No. of nodes in Level
            vector<int> level(n);
            for(int i=0;i<n;i++){
                TreeNode *node = q.front();
                q.pop();
                if(node->left) q.push(node->left);
                if(node->right) q.push(node->right);
                int index = (LeftToRight)?i:(n-1)-i;
                level[index]=node->val;
            }
            res.push_back(level);
            LeftToRight=!LeftToRight;
        }
        return res;
    }
};
```

TC:O(N) and SC:O(N)
