# Next Greater Element using Stack

[LeetCode](https://leetcode.com/problems/next-greater-element-i/)

Given an integer array A, return the next greater element for every element in A. The next greater element for an element x is the first element greater than x that we come across while traversing the array in a clockwise manner. If it doesn't exist, return -1 for this element.


## Brute Force using 2 Loops

Use one loop to traverse i=0->n-1 and other loop inside it as j=i+1->n-1 to look for greater element

## Better using stack

Traverse the array in reverse order and store the elements in stack, when current element is lesser than stack's top then it's the NGE of current array value

- When current val of array is greater than stack's top, then pop the top until you find element in stack which is greater than current val of array
- If stack becomes/is empty then -1 is your answer
- Then put/push current array value in stack

> Answer array is in ascending order from left to right

```cpp
class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& nums1,vector<int>& nums2) {
        unordered_map<int,int> mp; // Will store {val of nums2, it's NGE}
        stack<int> st; //To get next greater

        for(int i = nums2.size()-1; i >= 0; i--) {
            while(!st.empty() && st.top() <= nums2[i]) {
                st.pop();
            }
            mp[nums2[i]] = st.empty() ? -1 : st.top();
            st.push(nums2[i]); //Remember to push current ele in Stack
        }
        vector<int> ans; //To return NGE of nums1 specific vals
        for(int x : nums1) {
            ans.push_back(mp[x]);
        }
        return ans;
    }
};
```

TC=O(M for traversing all eles of nums2 + M for popping elements from stack) = O(2M)

SC=O(M for map + N for returning nums1's NGE only)= O(M+N)
