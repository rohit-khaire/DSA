# Rotate a LL

Given the head of a linked list, rotate the list to the right by k places.

Rotate to right by K places or K Times.

[LeetCode](https://leetcode.com/problems/rotate-list/description/)

## Brute Force

Straight forward, k times removing last Node and attaching it to head and making it as new head.

## OPTIMAL APPROACH by making LL Cyclic

Instead of performing ``k`` individual rotations, we observe that rotating a list by its own length times ( List woth length 3, if rotated 3 times becomes same list again) results in the same list. So, we only need to rotate by k % length.
We first compute the length of the list and connect the last node to the head, forming a circular linked list. 
Then we locate the new tail, which is at length - (k % length) steps from the start. The node next to this becomes the new head, and we break the circular link there. This transforms the list in a single traversal, making the process efficient.

- Handle edge cases where the list is empty, has one node, or k is 0 — in these cases, return head as-is.
- Traverse the list to calculate its total length.
- Connect the last node to the first node, converting the list into a circular linked list.
- Calculate effective rotations as k % length to avoid unnecessary full rotations.
- Find the new tail node, which is located at the (length - k % length ).
- Set the new head to the node just after the new tail.
- Break the circular link by setting newTail.next = null.
- Return the new head of the rotated list.

*Calculate length->find efficient val of k-> make LL circular-> Find no. of movements required to reach position of new tail->move tail to that position->make Node next to tail as head-> make tail's next as NULL*

<br>

```cpp
class Solution {
public:
    ListNode* rotateRight(ListNode* head, int k) {
        if(head==NULL || head->next==NULL || k==0) return head;
        ListNode *tail = head;
        int length=1; //consider head Node
        while(tail->next!=NULL){
            tail=tail->next;
            length++;
        }
        k=k%length; //Optimized no. of rotations
        int movements=length-k; //3-1=2, that 2nd is tail and next of it is head
        tail->next=head; // cyclic LL
        while(movements){
            tail=tail->next;
            movements--;
        }
        head=tail->next;
        tail->next=NULL;
        return head;
    }
};
```

Finding length and tail => Traverses entire list once => O(n)

while(movements) => Traverses length-k nodes => O(n) in worst case

O(N+N)=2N 

**TC=O(N) and SC=O(1)**
