# Linked List Cycle II

Detect the cycle and return the entry point (duplicate/common node)

[LeetCode](https://leetcode.com/problems/linked-list-cycle-ii/)

We use Floyd's Cycle Detection Algorithm to find the detection

If fast or fast->next is null, then there is no cycle

Slow moves by 1 step and fast moves by 2 steps

If there is cycle, then there will be a Node at which fast==slow, then
- We point slow to head, and fast still points to collided Node
- Move slow and fast by 1-1 step till they becomes equal fast==slow
- When fast==slow, that is the entry point of Cycle, return it

```cpp
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        if(head==NULL) return head;
        ListNode *slow=head, *fast=head;
        while(fast && fast->next){
            slow=slow->next;
            fast=fast->next->next;
            if(slow==fast){
                slow=head;
                while(slow!=fast){
                    slow=slow->next;
                    fast=fast->next;
                }
                return slow;
            }
        }
        return NULL;
    }
};
```

### Time Complexity (TC): **O(N)**

* In the first phase (Floyd's Cycle Detection), `slow` and `fast` together traverse at most `N` nodes before either meeting or reaching the end.
* If a cycle exists, in the second phase both pointers move one step at a time to find the cycle's starting node, taking at most `N` more steps.

Overall:

[
O(N) + O(N) = O(2N)
]

**TC = O(N)**

---

### Space Complexity (SC): **O(1)**

**SC = O(1)**

---

### One-Line Interview Answer

**TC:** `O(N)` because the list is traversed at most a constant number of times.
**SC:** `O(1)` because only two pointers are used.
