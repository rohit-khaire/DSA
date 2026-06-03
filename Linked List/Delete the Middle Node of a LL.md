# Delete the Middle Node of a LL

[LeetCode](https://leetcode.com/problems/delete-the-middle-node-of-a-linked-list/)

Find the middle using Tortoise and Hare algo, then delete that slow node. For that purpose we would also require previous node of slow for new linking procedure.

**In LeetCode, no deleting(no free up of space is required manually) This happens automatically at the end**

Beats 100%

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
    ListNode* deleteMiddle(ListNode* head) {
        if(head==NULL) return NULL;
        if(head->next==NULL){
            delete head;
            return NULL;
        }
        ListNode *slow=head;
        ListNode *fast=head;
        ListNode *prevSlow =NULL;  //previous element of slow
        while(fast!=NULL && fast->next!=NULL){
            prevSlow = slow;
            slow=slow->next;
            fast=fast->next->next;
        }
        //slow is mid element
        prevSlow->next=slow->next;
        delete slow;
        return head;

    }
};
```

**TC=O(N/2) and SC=O(1)**
