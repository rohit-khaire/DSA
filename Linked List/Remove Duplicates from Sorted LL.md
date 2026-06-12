# Remove Duplicates from Sorted LL

[LeetCode](https://leetcode.com/problems/remove-duplicates-from-sorted-list/)





Remove Duplicates from Sorted List. The key idea is:

- prev points to the last unique node kept in the result.
  
- curr scans the list.
  
- When curr->val == prev->val, the duplicate is skipped by advancing curr.
  
- When values differ, prev->next = curr links the next unique node, then both pointers advance.
  
- Finally, prev->next = NULL cuts off any trailing duplicate chain.

- Imagine it for [1,1,1]

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
    ListNode* deleteDuplicates(ListNode* head) {
        if(head==NULL || head->next==NULL) return head;
        ListNode *prev=head;
        ListNode *curr=head->next;
        while(curr){
            if(curr->val==prev->val){
                curr=curr->next; //You can delete curr node while skipping
            }else{
                prev->next=curr;
                prev=curr;
                curr=curr->next;
            }
        }
        prev->next=NULL;
        return head;
    }
};
```

TC=O(N) and SC=O(1)
