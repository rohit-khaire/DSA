# Convert Sorted Array to Binary Search Tree

[LeetCode](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/description/)

# Approach - Recursive

As the array is sorted, if you try to create the BST Directly, then it can become skewed

- We recursively get the mid, and then create it as Root Node
- for left subtree, we call same function by passing array from left to mid-1
- for right subtree, we call same function by passing array from mid+1 to right
- and return the root
- **Base Condition:** We stop (Start returning NULL) when left becomes > than right


```cpp
class Solution {
public:
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        return build(nums,0,nums.size()-1);
    }
    TreeNode* build(vector<int> &arr, int left, int right){
        if(left>right) return NULL;
        int mid = left+(right-left) /2;
        TreeNode *root = new TreeNode(arr[mid]);
        root->left = build(arr,left,mid-1);
        root->right = build(arr,mid+1,right);
        return root;
    }
};
```

TC:O(N) and SC:O(H)

We recursively get the middle and make it as root, so that our tree is balanced.
