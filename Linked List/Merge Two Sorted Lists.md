# Merge Two Sorted Lists

[LeetCode](https://leetcode.com/problems/merge-two-sorted-lists/)

We have two sorted LLs, and we want to merge them

## Brute Force

Use external space like Array to store the elements in a sorted manner

Or else store all the elements of l1 and l2, and then sort the Array

Then convert that Array to LL

# OPTIMAL Solution (In-place)

Just change the linkings using next element of Node

Keep l1 as always smaller element, and Keep track of previous element of l1 for linking purpose 

when l1 become greater swap l1 and l2

<img width="654" height="428" alt="image" src="https://github.com/user-attachments/assets/25bb7fc2-f3b2-4995-8f4f-f2b7bf528583" />

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(l1==NULL) return l2;
        if(l2==NULL) return l1;
        ListNode *res;
        if(l1->val > l2->val){
            swap(l1,l2); //So that l1 remains always small
        }
        res=l1;
        ListNode *prevL1=NULL;
        while(l1 && l2){
            while(l1!=NULL && l1->val <= l2->val){
                prevL1=l1;
                l1=l1->next;
            }
            prevL1->next=l2;
            swap(l1,l2); //As l1->val > l2->val, and we always want l1 to be smaller
        }
        return res;
    }
};
```


**TC=O(N+M) and SC=O(1)**

