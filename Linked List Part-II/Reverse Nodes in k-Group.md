# Reverse Nodes in k-Group

[LeetCode](https://leetcode.com/problems/reverse-nodes-in-k-group/)

```cpp
class Solution {
public:
    // Helper function to find the k-th node from the current node
    ListNode* getKthNode(ListNode* curr, int k) {
        while (curr && k > 0) {
            curr = curr->next;
            k--;
        }
        return curr;
    }

    ListNode* reverseKGroup(ListNode* head, int k) {
        ListNode *dummy = new ListNode(0,head);
        ListNode *prevGrp = dummy;
        while(true){
            ListNode *kth = getKthNode(prevGrp,k);
            if(kth==NULL) break;
            ListNode *nextGrp = kth->next;
            ListNode *prev=nextGrp; //So that 1st node points directly to next Grp instead of 
            ListNode *curr=prevGrp->next; 
            for (int i = 0; i < k; i++) {
                ListNode* nxt = curr->next;
                curr->next = prev;
                prev = curr;
                curr = nxt;
            }
            // Connecting previous group to the reversed group
            ListNode* temp = prevGrp->next;
            prevGrp->next = kth;
            prevGrp = temp;
        }
        // Returning the new head
        return dummy->next;
    }

};
```

