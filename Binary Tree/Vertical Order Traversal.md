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
```

-------------

# Full Explanation for Understanding

This is one of the most confusing parts of Vertical Traversal. Let's build the visualization from scratch.

---

# Step 1: What coordinates are being stored?

For every node:

```
Root = (0,0)

Left Child  = (x-1, y+1)
Right Child = (x+1, y+1)
```

Example:

```
        1(0,0)
       /      \
  2(-1,1)   3(1,1)
```

Now a bigger tree:

```
            1(0,0)
          /        \
     2(-1,1)      3(1,1)
      /   \        /   \
 4(-2,2) 5(0,2) 6(0,2) 7(2,2)
```

Notice something important:

```
5 -> (0,2)
6 -> (0,2)
```

Both nodes occupy the SAME position.

This is exactly why things become tricky.

---

# Step 2: What does the map store?

```cpp
map<int, map<int, multiset<int>>> nodes;
```

Let's break it layer by layer.

---

## First map

```cpp
map<int, ...>
```

Key = x (vertical line)

Example:

```
x = -2
x = -1
x =  0
x =  1
x =  2
```

Map automatically keeps them sorted:

```
-2 -> ...
-1 -> ...
 0 -> ...
 1 -> ...
 2 -> ...
```

This guarantees leftmost vertical appears first.

---

## Second map

```cpp
map<int, multiset<int>>
```

Inside every vertical line:

Key = y (level)

Example:

```
x = 0

0 -> {1}
2 -> {5,6}
```

Again map keeps levels sorted:

```
0
1
2
3
...
```

So top node comes before lower node.

---

## Third container

```cpp
multiset<int>
```

Stores all node values having SAME x and SAME y.

Example:

```
5 -> (0,2)
6 -> (0,2)
```

Then:

```cpp
nodes[0][2]
```

contains

```
{5,6}
```

---

# Visualizing the whole structure

For tree:

```
            1
          /   \
         2     3
          \   /
           5 6
```

Coordinates:

```
1 -> (0,0)

2 -> (-1,1)
3 -> (1,1)

5 -> (0,2)
6 -> (0,2)
```

Stored as:

```
nodes

{
    -1 :
    {
        1 : {2}
    },

     0 :
     {
         0 : {1},
         2 : {5,6}
     },

     1 :
     {
         1 : {3}
     }
}
```

This is exactly how the map looks.

---

# Step 3: Why not just use set?

A normal set:

```cpp
set<int>
```

Properties:

* Sorted
* Unique elements only

Example:

```cpp
set<int> s;

s.insert(5);
s.insert(5);
```

Result:

```
{5}
```

Duplicate removed.

---

But in a tree, duplicate values can exist.

Example:

```
      1
     / \
    5   5
```

Suppose both end up at same coordinate.

We need:

```
{5,5}
```

not

```
{5}
```

So set is wrong.

---

# Step 4: Why multiset?

Multiset:

```cpp
multiset<int>
```

Properties:

* Sorted
* Duplicates allowed

Example:

```cpp
multiset<int> ms;

ms.insert(5);
ms.insert(5);
ms.insert(3);
```

Result:

```
{3,5,5}
```

Exactly what Vertical Traversal requires.

---

# Step 5: Why not vector?

You absolutely can store:

```cpp
vector<int>
```

But vector does NOT sort automatically.

Example:

```cpp
vector<int> v;

v.push_back(6);
v.push_back(5);
```

Result:

```
[6,5]
```

Problem statement says:

When nodes have same x and same y:

> Sort according to node value.

Expected:

```
[5,6]
```

Vector gives:

```
[6,5]
```

unless you manually do:

```cpp
sort(v.begin(), v.end());
```

after traversal.

---

# Why multiset is preferred?

Instead of:

```cpp
vector<int>
```

and later

```cpp
sort(...)
```

we simply do:

```cpp
multiset.insert(...)
```

and it remains sorted automatically.

---

# Step 6: What happens when same x but different y?

Example:

```
        1
       /
      2
       \
        5
```

Coordinates:

```
1 -> (0,0)

2 -> (-1,1)

5 -> (0,2)
```

For x = 0:

```
(0,0) -> 1
(0,2) -> 5
```

Output should be:

```
1 before 5
```

Because y=0 comes before y=2.

That's why second map exists.

---

# Step 7: What happens when same x and same y?

Example:

```
        1
       / \
      2   3
       \ /
        5 6
```

Coordinates:

```
5 -> (0,2)
6 -> (0,2)
```

Both share:

```
x = 0
y = 2
```

Rule:

```
Sort by value
```

If values are:

```
6 and 5
```

Output:

```
5 6
```

Hence:

```cpp
multiset<int>
```

---

# Why BFS?

Many students think BFS is required for ordering.

Actually:

❌ Not for sorting.

The maps and multiset already handle ordering.

BFS is mainly used because:

* Easy to carry coordinates
* Easy level-wise traversal
* No recursion depth issues

DFS can also solve it.

---

# Final Mental Model

Think of the structure as:

```cpp
map<
    x,
    map<
        y,
        multiset<node values>
    >
>
```

or visually:

```
Vertical Line (x)
│
├── Level (y)
│     │
│     └── Sorted Node Values
│
├── Level (y)
│     │
│     └── Sorted Node Values
```

Example:

```
x=-1
   y=1 -> {2}

x=0
   y=0 -> {1}
   y=2 -> {5,6}

x=1
   y=1 -> {3}
```

So the data structures solve three different sorting requirements:

| Data Structure  | Purpose                                                 |
| --------------- | ------------------------------------------------------- |
| `map<x,...>`    | Left vertical → Right vertical                          |
| `map<y,...>`    | Top level → Bottom level                                |
| `multiset<int>` | Same position nodes sorted by value, duplicates allowed |

This is the key insight behind why the solution uses:

```cpp
map<int, map<int, multiset<int>>> nodes;
```

Each layer solves exactly one ordering requirement from the problem statement. 

---------------

This final step is simply **unpacking the nested map structure into the answer vector**.

Let's use the exact structure we discussed.

Suppose after BFS, `mpp` contains:

```cpp
{
    -1 :
    {
        1 : {2}
    },

     0 :
     {
         0 : {1},
         2 : {5,6}
     },

     1 :
     {
         1 : {3}
     }
}
```

---

# First Loop

```cpp
for(auto p : mpp)
```

`p` represents one vertical line (`x`).

### Iteration 1

```cpp
p.first = -1

p.second =
{
    1 : {2}
}
```

Create:

```cpp
vector<int> temp;
```

---

# Second Loop

```cpp
for(auto q : p.second)
```

Now we're traversing levels (`y`) inside this vertical.

### Iteration

```cpp
q.first = 1

q.second = {2}
```

---

# Third Loop

```cpp
for(auto val : q.second)
```

Traversing the multiset.

```cpp
val = 2
```

```cpp
temp.push_back(2);
```

Now:

```cpp
temp = [2]
```

---

After inner loops finish:

```cpp
res.push_back(temp);
```

Result:

```cpp
res =
[
    [2]
]
```

---

# Next Vertical

Now:

```cpp
p.first = 0

p.second =
{
    0 : {1},
    2 : {5,6}
}
```

Create:

```cpp
temp = []
```

---

## First level

```cpp
q.first = 0
q.second = {1}
```

Add:

```cpp
temp = [1]
```

---

## Second level

```cpp
q.first = 2
q.second = {5,6}
```

Remember:

```cpp
multiset = {5,6}
```

already sorted.

Loop:

```cpp
val = 5
```

```cpp
temp = [1,5]
```

Then:

```cpp
val = 6
```

```cpp
temp = [1,5,6]
```

---

Push into result:

```cpp
res =
[
    [2],
    [1,5,6]
]
```

---

# Last Vertical

```cpp
p.first = 1

p.second =
{
    1 : {3}
}
```

Produces:

```cpp
temp = [3]
```

Push:

```cpp
res =
[
    [2],
    [1,5,6],
    [3]
]
```

---

# Visual Representation

Think of `mpp` as a 3-floor building:

```text
Vertical x = -1
    Level y = 1
        Values = {2}

Vertical x = 0
    Level y = 0
        Values = {1}

    Level y = 2
        Values = {5,6}

Vertical x = 1
    Level y = 1
        Values = {3}
```

The loops simply flatten it:

```text
x=-1  -> [2]

x=0   -> [1,5,6]

x=1   -> [3]
```

Final answer:

```cpp
[
    [2],
    [1,5,6],
    [3]
]
```

### One-line interpretation of each loop

```cpp
for(auto p : mpp)
```

➡️ Pick one vertical column.

```cpp
for(auto q : p.second)
```

➡️ Traverse levels from top to bottom in that column.

```cpp
for(auto val : q.second)
```

➡️ Traverse all nodes at the same position (already sorted by multiset).

That's all this final step is doing: **Map → Levels → Values → Answer Vector**. 
