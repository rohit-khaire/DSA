# Top View of Binary Tree

Get all the elements which you can see from top of the Binary Tree

# Approach

We Imagine a Level Wise tree, but levels will be vertical, Like below:
<img width="1780" height="1019" alt="image" src="https://github.com/user-attachments/assets/3c31ee92-159f-4e51-be9a-b0fc84a0572a" />
**Output: Top View: [4, 2, 1, 3, 11]**

Have a map<int,Node> this stores results. Node and it's level. Map can help we get that if that level is already done or not by finding level in it.

To imagine the Binary Tree from above, we visualise vertical lines passing through the tree. Each vertical line represents a unique vertical position. Nodes to the right of the tree’s centre are assigned positive vertical indexes. As we move to the right, the vertical index increases. Nodes to the left of the tree’s centre are assigned negative vertical indexes. As we move to the left, the vertical index decreases.

<br>

We use a map data structure to store the nodes corresponding to each vertical level of the tree as the map automatically sorts the elements based on their ascending value. Against each vertical level, the node highest in the tree at that vertical level is added by traversing the tree level order wise (BFS).

- Create a vector `ans` to store the result. Check if the tree is empty. If it is, return an empty vector.
- Create a map to store the top view of nodes based on their vertical positions. The key of this map is the vertical index and the value is the node’s data.
- Initialise a queue to perform breadth first traversal. Each element of this queue is the node of the binary tree along with its vertical coordinate. Enqueue the root node into the queue with its vertical position initialised to 0.

**While the queue is not empty, pop the front node of the queue and for this node:**

- Get its vertical position. If this vertical position is not in the map, add the node’s data to the map. This means that this node is the first node encountered at this vertical position during the traversal.
- If the vertical position of this node is already a key in the map, it implies that a node higher in the tree with the same vertical position has already been processed.
- Enqueue the left child with a decreased vertical position ie. current vertical index -1. As when we move to the left child, we are moving towards the left column in the vertical order traversal.
- Enqueue the right child with an increased vertical position ie. current vertical index + 1. As when we move to the right child, we are moving towards the right column in the vertical order traversal.

**Iterate over the map and push the values of each node into the top view traversal.**

Since the keys of the map are sorted based on their keys (vertical positions), the nodes added to the `ans` vector will be sorted left to right.

Return the ‘ans’ vector.

**CODE:**

<br>

```cpp
class Solution {
public:
    // Function to return the top view of the binary tree
    vector<int> topView(Node* root) {
        // Create a vector to store the final answer
        vector<int> ans;

        // If the tree is empty, return an empty result
        if (root == NULL) {
            return ans;
        }

        // Create a map to store vertical level -> node value (only first encountered)
        map<int, int> mpp;

        // Create a queue for BFS that stores {node, vertical_level}
        queue<pair<Node*, int>> q;

        // Push the root node with vertical level 0
        q.push({root, 0});

        // Start BFS traversal
        while (!q.empty()) {
            // Extract the front element of the queue
            auto it = q.front();
            q.pop();

            // Get the node and its vertical position
            Node* node = it.first;
            int line = it.second;

            // If this vertical position is being visited for the first time, store it
            if (mpp.find(line) == mpp.end()) {
                mpp[line] = node->data;
            }

            // If there is a left child, push it with vertical level - 1
            if (node->left != NULL) {
                q.push({node->left, line - 1});
            }

            // If there is a right child, push it with vertical level + 1
            if (node->right != NULL) {
                q.push({node->right, line + 1});
            }
        }

        // Traverse the map and store values in the answer vector
        for (auto it : mpp) {
            ans.push_back(it.second);
        }

        // Return the result
        return ans;
    }
};
```

TC: O(N) for BFS + Each operation takes O(log K) in Map where K is the number of vertical lines. In the worst case (e.g., a completely skewed tree), K = N. so, N nodes × O(log N) = O(N log N) + For Map to Array Let width = W.Cost = O(W) & Since W ≤ N, this is O(N).

TC: O(N)+O(NlogN)+O(N) =O(NlogN)

SC: O(N)+O(N)+O(N) for Queue,Map and Answer Vector

