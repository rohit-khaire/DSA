# Average of Levels in Binary Tree

[Leetcode](https://leetcode.com/problems/average-of-levels-in-binary-tree/description/)

return vector with Average of each level

# Approach 

- Push the root into the queue.
- For each level:
  - Store the current queue size (size), which is the number of nodes at that level.
  - Traverse exactly size nodes.
  - Compute the sum of their values.
  - Push their left and right children into the queue.
- After processing the level, compute:
  - average = (double)sum / size;
- Repeat until the queue is empty.



> Note: Use long long sum to avoid integer overflow when summing many node values.

<br>

```cpp
class Solution {
public:
    vector<double> averageOfLevels(TreeNode* root) {
        vector<double> ans;
        queue<TreeNode*> q;
        q.push(root);

        while (!q.empty()) {
            int size = q.size();
            long long sum = 0;

            for (int i = 0; i < size; i++) {
                TreeNode* node = q.front();
                q.pop();

                sum += node->val;

                if (node->left)
                    q.push(node->left);
                if (node->right)
                    q.push(node->right);
            }

            ans.push_back((double)sum / size);
        }

        return ans;
    }
};
```

TC:O(N) & SC:O(W) (where ``w`` is the maximum width of the tree)
