# Add Two Numbers of LL

[LeetCode](https://leetcode.com/problems/add-two-numbers/)

## OPTIMAL SOLUTION ONLY, no brute available 

### Short & Simple Algorithm

1. Create a **dummy node** and point `temp` to it.
2. Initialize `carry = 0`.
3. Repeat while `l1`, `l2`, or `carry` exists:

   * Start `sum = carry`.
   * If `l1` exists, add its value to `sum` and move `l1` ahead.
   * If `l2` exists, add its value to `sum` and move `l2` ahead.
   * Store new carry: `carry = sum / 10`.
   * Create a node with digit: `sum % 10`.
   * Attach it to the answer list and move `temp` ahead.
4. Return `dummy.next` (head of the result list).

### One-Line Memory Trick

**"Add digits + carry → save remainder as node → save quotient as carry → repeat until everything ends."**

### Example

```text
2 -> 4 -> 3
5 -> 6 -> 4
```

```text
2+5 = 7      → node 7
4+6 = 10     → node 0, carry 1
3+4+1 = 8    → node 8
```

Result:

```text
7 -> 0 -> 8
```


```cpp
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {

        ListNode dummy;
        ListNode* temp = &dummy;

        int carry = 0;

        while(l1 || l2 || carry) {

            int sum = carry;

            if(l1) {
                sum += l1->val;
                l1 = l1->next;
            }

            if(l2) {
                sum += l2->val;
                l2 = l2->next;
            }

            carry = sum / 10;

            temp->next = new ListNode(sum % 10);
            temp = temp->next;
        }

        return dummy.next;
    }
};
```
**TC and SC = O(max(m, n))**
