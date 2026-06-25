# Diameter of Binary Tree

[LeetCode](https://leetcode.com/problems/diameter-of-binary-tree/)

 Given the root of the Binary Tree, return the length of its diameter. The Diameter of a Binary Tree is the longest distance between any two nodes of that tree. This path may or may not pass through the root.

 # Approach

Using Recursion to get left height and right height of current Node and then form a Width using left+right, we will store this maximum value of left+right

Now choose max height from left and right, as parent node will have that much of one side(either left of right) height +1

+1 is used as height between current node and parent is 1

So parent will have maximum height from left and max height from right, left + right = Max path possible using current node in between to form a path


# Algorithm
- Have global maxi to store the maximum width or maximum path possible using current node, and a recursive function findMax
  - if root is NULL, return 0, imagine a leaf node, where left height and right height comes as 0
  - get left height of root using root->left
  - get right height of root using root->right
  - store maximum width max(maxi, left+right), left+right forms a path/width
  - return maximum height from left or right +1, +1 refers as distance between current node and root node is 1

<br><br>

```
1. Initialize diameter = 0.

2. Create a recursive function height(node):

   a. If node is NULL:
         return 0

   b. Find leftHeight = height(node->left)

   c. Find rightHeight = height(node->right)

   d. Update:
         diameter = max(diameter,
                        leftHeight + rightHeight)

   e. Return:
         1 + max(leftHeight, rightHeight)

3. Call height(root).

4. Return diameter.
```

<br><br>

CODE:

 ```cpp
class Solution {
public:
    int findMax(TreeNode * root, int &maxi){
        if(root==NULL) return 0; //return 0 when going ahead of leaf
        int left = findMax(root->left,maxi); //left height
        int right = findMax(root->right,maxi); //right height
        maxi = max(maxi,left+right); //stroing max width found till now (l+r=width or path including current node)
        return 1 + max(left,right); //Distance between parent and me is 1, can't have left and right both now, so have max of them to get max width further

    }
    int diameterOfBinaryTree(TreeNode* root) {
        int maxi=0;
        int maxFromLeftOrRightPlus1 = findMax(root,maxi);
        return maxi;
    }
};
```

- TC:O(N) and SC:O(H)
