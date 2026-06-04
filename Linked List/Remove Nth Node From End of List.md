# Remove Nth Node From End of List

[LeetCode](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/)

Delete the Nth noode, but Nth node from the End

## Brute Force

Use a counter to get the length of LL, and then delete the Length-N+1 th Node

**TC near 2N**

## OPTIMAL 

Have a slow and a fast pointer, initially pointing the head.

Make fast pointer move N nodes ahaed, creating a distance of N-1 nodes between slow and fast

<img width="382" height="139" alt="image" src="https://github.com/user-attachments/assets/3057086c-18bb-4ca4-a768-c7b8488d8ef2" />

Now if fast becomes == NULL, which means head is to be deleted, delete the head

OR else

Now move both slow and fast 1 step each

<img width="409" height="163" alt="image" src="https://github.com/user-attachments/assets/582edce7-ef3a-4b53-a180-f94258f4d377" />

Now node next to slow is to be deleted

```cpp
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        if(head == NULL) return NULL;

        ListNode* slow = head;
        ListNode* fast = head;

        for(int i = 0; i < n; i++) {
            fast = fast->next;
        }

        if(fast == NULL)
            return head->next;

        while(fast->next) {
            slow = slow->next;
            fast = fast->next;
        }

        slow->next = slow->next->next;

        return head;
    }
};
```

**TC=O(N) and SC=O(1)**


*You can also have a dummy node as head to naturally handle edge cases like head to be deleted*


| Case                   | Expected     | Your Code |
| ---------------------- | ------------ | --------- |
| `head = NULL`          | `NULL`       | ✅         |
| `1`, `n=1`             | `NULL`       | ✅         |
| `1->2`, `n=1`          | `1`          | ✅         |
| `1->2`, `n=2`          | `2`          | ✅         |
| `1->2->3->4->5`, `n=1` | `1->2->3->4` | ✅         |
| `1->2->3->4->5`, `n=2` | `1->2->3->5` | ✅         |
| `1->2->3->4->5`, `n=3` | `1->2->4->5` | ✅         |
| `1->2->3->4->5`, `n=4` | `1->3->4->5` | ✅         |
| `1->2->3->4->5`, `n=5` | `2->3->4->5` | ✅         |

