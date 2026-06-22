# Right or Left Side View

[LeetCode](https://leetcode.com/problems/binary-tree-right-side-view/description/)

Right side view of Binary Tree:
<img width="1000" height="708" alt="image" src="https://github.com/user-attachments/assets/e7b3399d-8260-423e-8e19-4186068a367b" />

Input: root = [1,2,3,null,5,6,null,4]

The output would be: [1,3,6,4]

# Approach for right side view

Pre-order Traversal: Root - Left - Right

Reverse Pre-order: Right - Left - Root

Can solve this by traversing in Level Wise (like BFS but in reverse) and your first element will be your result, but it will also take same TC and SC

Hence solving using DFS (Root-Right-Left) and match level using arr.size() and input parameter level value


## Recursive approach

<img width="638" height="393" alt="image" src="https://github.com/user-attachments/assets/f192497b-0854-4179-b33c-1e72e581ae49" />

PseudoCode:
```cpp
f(root,level){  //have a ds that stores result, it's size can be used to get the level we have covered
  if(node==NULL) return;
  if(level==ds.size()) ds.push(node); //coming to this level for first time
  f(node->right,level+1);
  f(node->left,level+1);
}
```

For the given tree:

```text
          1
        /   \
       2     3
      / \     \
     4   5     7
        /
       6
```

Let's dry run your code:

```cpp
void rightSide(TreeNode *root, int level, vector<int> &res){
    if(root==NULL) return;

    if(level==res.size())
        res.push_back(root->val);

    rightSide(root->right,level+1,res);
    rightSide(root->left,level+1,res);
}
```

---

# Initial Call

```cpp
rightSide(1,0,res)
```

```text
res = []
level = 0

0 == res.size() (0)
Add 1

res = [1]
```

Go Right:

---

# Node 3

```cpp
rightSide(3,1,res)
```

```text
res = [1]
level = 1

1 == res.size() (1)
Add 3

res = [1,3]
```

Go Right:

---

# Node 7

```cpp
rightSide(7,2,res)
```

```text
res = [1,3]
level = 2

2 == res.size() (2)
Add 7

res = [1,3,7]
```

Right = NULL

Left = NULL

Return to 3

Left of 3 = NULL

Return to 1

---

# Node 2

```cpp
rightSide(2,1,res)
```

```text
res = [1,3,7]
level = 1

1 != res.size() (3)

Do NOT add
```

Go Right:

---

# Node 5

```cpp
rightSide(5,2,res)
```

```text
res = [1,3,7]
level = 2

2 != res.size() (3)

Do NOT add
```

Go Right = NULL

Go Left:

---

# Node 6

```cpp
rightSide(6,3,res)
```

```text
res = [1,3,7]
level = 3

3 == res.size() (3)

Add 6

res = [1,3,7,6]
```

Return to 5

Return to 2

---

# Node 4

```cpp
rightSide(4,2,res)
```

```text
res = [1,3,7,6]
level = 2

2 != res.size() (4)

Do NOT add
```

Return

---

# Traversal Order

Because we visit **Right before Left**, the traversal is:

```text
1
├── 3
│   └── 7
└── 2
    └── 5
        └── 6
    └── 4
```

Actual visit sequence:

```text
1 → 3 → 7 → 2 → 5 → 6 → 4
```

---

# Final Answer

```cpp
[1,3,7,6]
```

### Why 6 appears?

At level 3, there is **only one node (6)**. Even though it is in the left subtree, it is still visible from the right side because no node exists at that depth on the right side.

```text
Right View:

Level 0 -> 1
Level 1 -> 3
Level 2 -> 7
Level 3 -> 6
```

✅ Output = **[1, 3, 7, 6]**

- TC: O(N) and SC: O(H) but in worst case (skewed Tree) O(N)

- In Balanced Tree: H = logN


