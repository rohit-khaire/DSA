# Remove Linked List Elements

[LeetCode](https://leetcode.com/problems/remove-linked-list-elements/)

Given the head of a linked list and an integer val, remove all the nodes of the linked list that has Node.val == val, and return the new head.

# MY SOLUTION which beats 100%

Have a dummy Node to get head deleted naturally, point dummy's next to head.

Have temp pointer pointing to Head and Prev pointer pointing to Dummy

Now start iterating the LL while(temp!=NUL)

when temp->val becomes equals to input val, means current temp node is the node which is to be deleted.

So just make prev's next point to temp's next

Move temp ahead and *Move prev only when temp was not equals to val*

When temp deletes any node, at that time prev remains same for temp's next

```cpp
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        if(head==NULL) return head;
        ListNode dummy(0,head);
        ListNode *prev=&dummy;
        ListNode *temp=head;
        while(temp!=NULL){
            if(temp->val==val){
                prev->next=temp->next;
            }
            else{
                prev=temp;
            }
            temp=temp->next;
        }
        return dummy.next;
    }
};
```

**TC=O(N) and SC=O(1)**
