# BT Maximum Path Sum

[LeetCode](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

Find the path that gives you maximum SUM. 

> The path can be without Root in it. Also it can end anywhere in-betwwen, no need to end it only on Leaf Nodes.

The path can stop anywhere.

# Approach

We will be using Recursion.

We can return Sum , instead of Height. And keep one Maxi variable to keep track of Maximum sum till now.

**Completely ignore Negatives**

<img width="275" height="239" alt="image" src="https://github.com/user-attachments/assets/b49354aa-6d6c-4df4-b0ea-5edc3f7151d8" />

Max sum here is: 45

- If root is Null, return 0;
- get left sum by selecting maximum from 0 and recursive call to root->left. If left sum is Negative, we store 0 instead.
- get right sum by selecting maximum from 0 and recursive call to root->right. If right sum is Negative, we store 0 instead.
- select maximum from maxi and leftSum + current's value + rightSum , this is storing our final result.
- return max(leftSum, rightSum) + current's value.

```cpp
class Solution {
public:
    int paths(TreeNode *root, int &maxi){
        if(root==NULL) return 0;
        //Completely ignore Negatives so that I can get max
        int left = max(0,paths(root->left, maxi)); //getting sum from left
        int right = max(0,paths(root->right, maxi)); //getting sum from right
        maxi = max(maxi, left+ root->val + right); //sum including current node
        return max(left,right) + root->val;
    }
    int maxPathSum(TreeNode* root) {
        if(root==NULL) return 0;
        int maxi=INT_MIN;
        int sumOfPathHavingRootNode = paths(root,maxi);
        return maxi;
    }
};
```

TC: O(N) and SC:O(N)
