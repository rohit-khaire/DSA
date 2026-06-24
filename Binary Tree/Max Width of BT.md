# Max Width of BT

[LeetCode](https://leetcode.com/problems/maximum-width-of-binary-tree/)

<br>

<img width="696" height="314" alt="image" src="https://github.com/user-attachments/assets/5971f020-e9cd-45c7-9221-a065b124d9b7" />

Blue is Answer in above image

Return maximum width possible (if NULL between leftmost and rightmost nodes in a level are also nodes to be considered in Width)

# Approach using BFS

Using a BFS Approach as I need width of each level, so that I can choose max from that widths

We will be using BFS approach, in which we calculate width for each level, then we choose max from it

**Segment Tree** concept is using here, where we index each nodes

Each level's leftmost Node/NULL will be 0th index, and for that level indexes increases as 0,1,2,3,...

Width can be calculated as Last index in that level +1, for a particular level

<img width="656" height="401" alt="image" src="https://github.com/user-attachments/assets/6d5bdc90-53d0-4390-a99e-53b3c0b10064" />



- If root is NULL, then width is 0, return 0;
- Have a Queue for BFS Traversal, Queue stores {Node,it's index}
- Push the root in the Queue with index as 0, {root,0}
- Start a loop, while(!q.empty())
  - n= get No. of Nodes in current level (get size of queue)
  - s= Now our front Node's index (front's index) is the 1st Node in current level, get front's index
  - Start looping for each Node in current level, for (int i = 0; i < n;i++)
    - store the queue's front(whole pair {Node,index}) in Variable and pop it from Queue
    - get Normalized index of current Node (Current Node's Index - Minimum(First) Index of Current Level) => tmp.second-s
    - if current node is Last Node of current Level (i==n-1), store the normalized index as last index
    - if there is left child of Current Node, then push {left child, 2*normalizedIndex +1} in Queue
    - if there is right child of Current Node, then push {right child, 2*normalizedIndex +2} in Queue
  - Store width as max from width and last+1

```cpp
class Solution {
public:
    int widthOfBinaryTree(TreeNode* root) {
        if (root == nullptr)    return 0;
        queue<pair<TreeNode*, int>> q;
        q.push({root, 0});
        int w = 0;
        while (!q.empty()) {
            int n = q.size(); //No. of nodes in the level
            int s = q.front().second; //first index (mmin used to normalize values to 0,1,2) (Minimum index of the level = first index of level)
            int last;
            for (int i = 0; i < n; i++) {
                auto tmp = q.front();
                q.pop();
                long long int ind = tmp.second-s; //Normalized 0,1,2 children index
                if (i == n-1)   last = ind;
                if (tmp.first->left)  q.push({tmp.first->left, (ind)*2+1});
                if (tmp.first->right)  q.push({tmp.first->right, (ind)*2 + 2});
            }
            w = max(w, last+1);
        }
        return w;
    }
};
```

**TC: O(N) and SC: O(N)**
