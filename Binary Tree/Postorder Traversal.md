# Postorder Traversal

# Different than others

[LeetCode](https://leetcode.com/problems/binary-tree-postorder-traversal/)

> The difficulty is: When I reach a node, how do I know whether its right subtree has already been processed?

**Main Issue Here:** Here you get confused when returning to above nodes. For Example,

```

   5
 /  \
1    8

```

When returning to 5, we get confused on Can we process the 5 Now? Because I don't know, whether right(8) is processed or not

We get confused on we are returning from left or right? (from 1 or from 8?)

As we can print root(5) only after right is processed

Can solve this by keeping track of lastVisited.

We have 3 approaches for Postorder:
1. Recursion
2. Using 1 stack (store last visited node in a variable)
3. Using 2 Stacks, we store root node in s2, and left and right in s1, then we perform same for s1.top() (Loop it), Atlast we get root-right-left in s2, and on popping we get left-right-root


# Approach 1 : Using Recursion

Similar as Previous

```cpp
class Solution {
public:
    void postorder(TreeNode *root, vector<int> &res){
        if(root==NULL) return;
        postorder(root->left,res);
        postorder(root->right,res);
        res.push_back(root->val);
    }
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> res;
        postorder(root,res);
        return res;
    }
};
```


# Approach 2 : Using 1 Stack

1. Push all left nodes to stack.
2. Peek top from stack.
3. Right unvisited?
      Go right.
4. Otherwise:
      Push node as result.
      Mark as lastVisited.
      Pop.


```
Has the right subtree been processed?

YES  -> Output node
NO   -> Go right
```

<br><br>


```cpp
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> res;
        if(root==NULL) return res;
        stack<TreeNode*> s;
        TreeNode *node = root;
        TreeNode *lastVisited = NULL;
        //s: 1 2 
        //p: 4 
        while(node || !s.empty()){
            while(node){ //stops on left NULL, push all left nodes of new node
                s.push(node);
                node=node->left;
            }
            TreeNode *curr = s.top();
            if(curr->right && curr->right!=lastVisited){
                node=curr->right;
            }else{
                //process current node as either right is NULL or else it's visited
                res.push_back(curr->val);
                lastVisited=curr;
                s.pop();
            }
        }
        return res;

    }
};
```

# Appraoch 3 : Using 2 Stacks or Using 1 Stack and 1 Array (Reverse Array)

1. push root in stack
2. get top of stack, pop it and push in result
3. if left exists, then push it in stack.
4. if right exists, then push it in stack
5. Reverse whole array atlast



```cpp
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> res;

        if (!root) return res;

        stack<TreeNode*> st;
        st.push(root);

        while (!st.empty()) {
            TreeNode* node = st.top();
            st.pop();

            res.push_back(node->val);

            if (node->left)  //Process left first as Stack is LIFO, and we want right first on popping to maintain Root-Right-Left
                st.push(node->left);

            if (node->right)
                st.push(node->right);
        }

        reverse(res.begin(), res.end()); //Root-Right-Left -> Left-Right-Root

        return res;
    }
};
```
