# Vertical Order Traversal

[LeetCode](https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/description/)

# Solution Given by me

> This is not Main Solution

**Lacks only when X and Y (Vertical Line and Horizontal Line) are same for 2 nodes**

Needs to handle this by sorting the nodes by value, but I am not sorting as I am coming up with new solution that will automatically handle this as I will be having Multiset for this

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> verticalTraversal(TreeNode* root) {
        vector<vector<int>> res;
        if(root==NULL) return res;
        map<int, vector<int>> mpp; mpp; //level,values at that level
        queue<pair<int,TreeNode*>> q; //level,Node
        q.push({0,root});
        while(!q.empty()){
            int level = q.front().first;
            TreeNode *node = q.front().second;
            q.pop();
            mpp[level].push_back(node->val);
            if(node->left) q.push({level-1,node->left});
            if(node->right) q.push({level+1,node->right});
        }
        for(auto &it : mpp){
            res.push_back(it.second);
        }
        return res;
    }
};
```

# Main Solution 

Similar logic, just changes in Data Structure make it efficient

<img width="704" height="684" alt="image" src="https://github.com/user-attachments/assets/b290ccf0-d464-4ce3-9f41-e6d452363dd3" />

X represents Vertical Line/Level (x-axis) and Y represents Horizontal Line/Level (y-axis)

<img width="1230" height="520" alt="image" src="https://github.com/user-attachments/assets/722b9952-da15-4b6c-9f89-fcfd61ecdf10" />

If we are having root, then our left child will be at (verticalLevel-1,horizontalLevel+1)

All elements can be given as:

<img width="638" height="634" alt="image" src="https://github.com/user-attachments/assets/4487df6a-ab3d-46f5-baaa-05b6242eb073" />


**Most Important Data Structure:** Create an empty map to store the nodes based on their vertical and horizontal levels.The key of the map ‘x’ represents the vertical column, and the nested map uses ‘y’ as the key for the level. Initialise a ‘multiset’ to store node values at a specific vertical and level to ensure unique and sorted order of nodes.

So we will be having a Data Structure as

``map<int,___> `` to represent **Vertical Line (X)**

Inside it, we need something like, horizontalLine -> {NodeValues}

> Node values must be in sorted order, and values can be repeated, so have sorted+repeated values

Can be done using, ``map<int,multiset<int>>`` , so **int for Horizontal Lines (Y) and Multiset for Sorted+Duplicate Values**

We we get a Data Structure as ``map<int,map<int,multiset<int>>>``

<img width="1254" height="636" alt="image" src="https://github.com/user-attachments/assets/cd844abe-a6d2-41ba-a446-2a4d751d19a3" />

-----------

<br><br>

CODE:
```cpp
class Solution {
public:
    vector<vector<int>> verticalTraversal(TreeNode* root) {
        vector<vector<int>> res;
        if(root==NULL) return res;
        queue<pair<TreeNode*,pair<int,int>>> q; //{root,{vertLevel,horizLevel}}
        q.push({root,{0,0}});  // Initially Level (0,0)
        map<int,map<int,multiset<int>>> mpp; // stores vertLevel -> horLevel -> {2,3,3}
        //as vertLevel will contain multiple horiLevel which can be same for 2 nodes
        while(!q.empty()){  //Using BFS
            TreeNode *node = q.front().first;
            int x = q.front().second.first;
            int y = q.front().second.second;
            mpp[x][y].insert(node->val);
            q.pop();
            if(node->left){
                q.push({node->left,{x-1,y+1}});
            }
            if(node->right){
                q.push({node->right,{x+1,y+1}});
            }
        }
        //MOST IMP PART than traversal
        //map<int,map<int,multiset<int>>> mpp;
        // Now map has 
        //p   q   val
        //0->{0->{1}}
        // ->{2->{1,2}}
        for(auto p : mpp){
            vector<int>temp;
            for(auto q : p.second){
                for(auto val : q.second)
                {
                    temp.push_back(val);
                }
            }
            res.push_back(temp);
        }
        return res;
    }
};
```

TC:
```
mpp[x][y].insert(node->val)
=
O(log N)+O(log N)+O(log N)
=
O(log N)

and for BFS, for N nodes:
N × O(log N)
=
O(N log N)

and for final res building at Last:
O(N) as N nodes were stored


Total TC: O(N log N) + O(N)
```

SC:
```
Queue: O(N)

Map: O(N)

Result Vector: O(N)
``
