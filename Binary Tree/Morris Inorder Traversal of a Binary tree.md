# Morris Inorder Traversal of a Binary tree

[LeetCode](https://leetcode.com/problems/binary-tree-inorder-traversal/)

In normal inorder we take TC:O(n) and SC:O(n) of Stack

But in Morris, we take TC:O(N) and SC:O(1)

**It uses Threaded Binary Tree concept.**

A tree where leaf nodes are connected to inorder predecessor or inorder successor. These links are known as Threads.

# Approach

Left - Root - Right

Let's build a permanent Logic:


1) Where left is null

```
  1
/  \
x   2
```

At this case, we just:

- Print(root)
- Move to right

2) There exists left

**Before moving left, link the rightmost Node of left sub-tree to current Node**

Then curr pointer can go to left.

if(rightmost Node of left sub-tree is already pointing to curr) means threaded link already exists, so we remove the Thread

Once you remove the thread, you can move to right

How will I know that, accessed node is via normal link or using threaded link. I get confused on whether to go left or right/

So I just check in left is there any thread? Yes and the thread is pointing to itself, then this means we are on current node using that thread.

Remove that link and go to left.

# Morris Inorder Traversal

## Idea

Normally, Inorder Traversal needs:

* Recursion Stack → `O(H)`
* Explicit Stack → `O(H)`

Worst Case Space = O(N)

Morris Traversal avoids both by temporarily creating a **thread (link)** from the inorder predecessor back to the current node.

This allows us to return to a node after finishing its left subtree without using a stack.

---

# Time Complexity (TC)

### TC = O(N)

Reason:

Each node is processed at most **2 times**:

1. First time → Create thread.
2. Second time → Remove thread and visit.

So total operations:

```text
≤ 2N
```

Therefore:

```text
TC = O(N)
```

---

# Space Complexity (SC)

### SC = O(1)

Used variables:

```cpp
cur
prev
```

No:

* Recursion
* Stack
* Queue

Hence:

```text
SC = O(1)
```

---

# Key Observation

For every node there are only 2 possibilities:

### Case 1: No Left Child

```text
Visit Node
Go Right
```

Example:

```text
    5
     \
      7
```

Inorder:

```text
5 7
```

Since nothing exists on left, we can directly visit it.

---

### Case 2: Left Child Exists

Need to process left subtree first.

So:

```text
Find Inorder Predecessor
```

(Inorder predecessor = Rightmost node in left subtree)

Example:

```text
       5
      /
     3
      \
       4
```

For node `5`:

```text
Predecessor = 4
```

---

# Complete Algorithm

## Step 1

Start:

```cpp
cur = root
```

---

## Step 2

Repeat while:

```cpp
cur != NULL
```

---

## Step 3

If:

```cpp
cur->left == NULL
```

then:

```text
Visit current node
Move right
```

Code:

```cpp
res.push_back(cur->val);
cur = cur->right;
```

---

## Step 4

Else (left subtree exists)

Find predecessor.

```cpp
prev = cur->left;

while(prev->right!=NULL &&
      prev->right!=cur)
{
    prev = prev->right;
}
```

Move to rightmost node of left subtree.

---

## Step 5

If:

```cpp
prev->right == NULL
```

Means:

```text
Thread not created yet
```

Create thread:

```cpp
prev->right = cur;
```

Go left:

```cpp
cur = cur->left;
```

---

## Step 6

Else:

```cpp
prev->right == cur
```

Means:

```text
Thread already exists
```

We returned from left subtree.

Remove thread:

```cpp
prev->right = NULL;
```

Visit current node:

```cpp
res.push_back(cur->val);
```

Move right:

```cpp
cur = cur->right;
```

---

## Step 7

Repeat until:

```cpp
cur == NULL
```

Return answer.

---

# Mental Flow (Easy to Remember)

Whenever you see a node:

```text
Has Left ?
│
├── No
│     Print cur
│     Go Right
│
└── Yes
      Find Predecessor
      │
      ├── Thread Missing
      │      Create Thread
      │      Go Left
      │
      └── Thread Exists
             Remove Thread
             Print cur
             Go Right
```

---

# 6-Line Algorithm

```text
1. Start from root.
2. If left is NULL → Visit and go right.
3. Else find predecessor (rightmost node of left subtree).
4. If predecessor's right is NULL → Create thread and go left.
5. If predecessor's right points to current → Remove thread, visit current, go right.
6. Repeat until current becomes NULL.
```

This is the shortest algorithm you need to reconstruct your entire Morris Inorder solution during an interview.


# Code

```cpp

class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        //Morris Inorder which takes TC:O(N) and SC:O(1)
        vector<int> res;
        if(root==NULL) return res;
        TreeNode *cur = root;
        while(cur!=NULL){
            if(cur->left==NULL){
                res.push_back(cur->val); //        5          //Can also access threaded link
                cur=cur->right;           //    x       7
            }
            else{
                //I have left
                TreeNode *prev = cur->left;
                while(prev->right!=NULL && prev->right!=cur){ //link predecessor to current Node
                    prev=prev->right;
                }
                if(prev->right==NULL){ //No link was created, so create a one
                    prev->right=cur;
                    cur=cur->left;
                }else{
                    //There exists a link(thread). Means cur is accessed using it
                    prev->right=NULL; //Delete the already existing thread(link), bring BT to it's OG form
                    res.push_back(cur->val);
                    cur=cur->right;
                }

            }
        }
        return res;
    }
};
```


# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
**O(N)**

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
**O(1)**
