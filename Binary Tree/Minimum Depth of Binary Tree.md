# Minimum Depth of Binary Tree

[Leetcode](https://leetcode.com/problems/minimum-depth-of-binary-tree/)

Given a Binary Tree, return the depth (1 based indexing) of closest leaf to Root

Closest leaf to Root

# Approach - Using BFS

Core logic is:

```markdown
If tree is empty:
    return 0

Put root into queue
depth = 1

While queue is not empty:

    Process all nodes at current level

    If any node is a leaf:
        return depth

    Add children to queue

    depth++
```

<br>

```cpp
class Solution {
public:
    int minDepth(TreeNode* root) {
        if(root==NULL) return 0;
        queue<TreeNode*> q;
        q.push(root);
        int depth=1;
        while(!q.empty()){
            int size=q.size();
            while(size){
                TreeNode* front = q.front();
                q.pop();
                if(front->left==NULL && front->right==NULL){
                    return depth;
                }
                if(front->left){
                    q.push(front->left);
                }
                if(front->right){
                    q.push(front->right);
                }
                size--;
            }
            depth++;
        }
        return depth;
    }
};
```

TC:O(N) and SC:O(N)
