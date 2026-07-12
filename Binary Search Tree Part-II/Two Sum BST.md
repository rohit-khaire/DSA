# Two Sum BST

[LeetCode](https://leetcode.com/problems/two-sum-iv-input-is-a-bst/)

# Apprach - Brute using Array

- Perform Inorder traversal on BST and store it in Array (Array will contain all the numbers in Ascending order)
- Now we can perform 2 Sum on that Array
  - i points to left and j points to right
  - if i+j == k, return true
  - if i+j>k , then j--
  - else i++
 

# Approach - Brute using Set as Hash

- Perform dfs traversal on BST
- For each node, search is there exists currentValue-k value in Set, if this value (remaining) exists then remaining+currentValue becomes = k
- else store current Value


# Approach - OPTIMAL : Using 2 Stacks

- on BST left mark as i and right mark as j
- We store i values in Stack1 and j values in stack2
- for i parent/next value (Left chi next value) can be derived using left stack's top

```cpp
class BSTIterator {
    stack<TreeNode*> st;
    bool reverse;

public:
    BSTIterator(TreeNode* root, bool rev) {
        reverse = rev;
        pushAll(root);
    }

    void pushAll(TreeNode* node) {
        while (node) {
            st.push(node);
            if (reverse)
                node = node->right;
            else
                node = node->left;
        }
    }

    int next() {
        TreeNode* node = st.top();
        st.pop();

        if (!reverse)
            pushAll(node->right);
        else
            pushAll(node->left);

        return node->val;
    }
};

class Solution {
public:
    bool findTarget(TreeNode* root, int k) {
        if (!root) return false;

        BSTIterator l(root, false); // smallest
        BSTIterator r(root, true);  // largest

        int i = l.next();
        int j = r.next();

        while (i < j) {
            int sum = i + j;

            if (sum == k)
                return true;
            else if (sum < k)
                i = l.next();
            else
                j = r.next();
        }

        return false;
    }
};
```

 TC:O(N) & SC:O(H)
