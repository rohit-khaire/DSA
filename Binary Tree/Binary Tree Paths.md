# Binary Tree Paths

[LeetCode](https://leetcode.com/problems/binary-tree-paths/)

Given the root of a binary tree, return all root-to-leaf paths in any order.

A **leaf** is a node with **no children**.

# Approach Recursive

Using DFS : Preorder Traveral

- Keep a list to keep track of nodes in current path
- Another list of string to keep track of all the paths, store all the paths here

<br>
Algorithm:

- IF current node is NULL, return.
- Current node is not NULL, so push it in Nodes List (Nodes in Current Path)
- Check if current Node is Leaf Node? (Both right and left are NULL?)
  - YES , I am leaf node
  - create a Path String using vals in list nodes (Nodes in current path)
  - push this string (Current Path) to Result Vector (Path from root to This Leaf)
  - Now pop the current node from list of nodes, and return; As parent node don't have this child in it's path (Path from root to parent)
  - return;
- apply this same function Preorder to left child
- Apply this same function Preorder to right child
- remove the current node from list of nodes ( As parent node don't have this child in it's path (Path from root to parent))



```cpp
class Solution {
public:
    void preorder(TreeNode *root, vector<int> &nodes, vector<string> &res){
        if(root==NULL) return;
        nodes.push_back(root->val);
        if(root->left==NULL && root->right==NULL){
            string path = "";
            for(int i=0;i<nodes.size();i++){
                path+= to_string(nodes[i]);
                if(i<nodes.size()-1) path+="->";
            }
            res.push_back(path);
            nodes.pop_back();
            return;
        }
        preorder(root->left,nodes,res);
        preorder(root->right,nodes,res);
        nodes.pop_back();
    }
    vector<string> binaryTreePaths(TreeNode* root) {
        vector<int> nodes;
        vector<string> res;
        preorder(root,nodes,res);
        return res;
    }
};
```


<br>

| Complexity            | Value                                                                                              |
| --------------------- | -------------------------------------------------------------------------------------------------- |
| Time Complexity       | **O(N + TotalCharactersInOutput)**                                                                 |
| Simplified Worst Case | **O(N²)** if you count total path-string generation across pathological trees with many long paths |
| Balanced Tree         | **O(N log N)**                                                                                     |
| Skewed Tree           | **O(N)**                                                                                           |
| Auxiliary Space       | **O(H)**                                                                                           |
| Worst Case Space      | **O(N)**                                                                                           |
| Output Space          | **O(TotalCharactersInOutput)**                                                                     |
