# Find intersection of Two Linked Lists

[LeetCode](https://leetcode.com/problems/intersection-of-two-linked-lists/)

Problem Statement: Given the heads of two singly linked-lists headA and headB, return the node at which the two lists intersect. If the two linked lists have no intersection at all, return null.

We cannot determine the intersection by Node's Value. We can determine the intersection using the Node itself (Address of Node).

## Brute Force using 2 loops

Using 2 loops one inside another we can get the solution

```cpp
for(headA->NULL){
  for(headB->NULL){
    if(headA==headB) return headA; // search for headA in LL headB
    headB=headB->next;
  }
  headA=headA->next;
}
return NULL;
```

For each element of headA, search for it in LL headB. If we found same elements in both, we can say that We found the intersection.

**TC=O(m*n) and SC=O(1)**

## Better Solution using HashSet

Using HashSet to store the addresses of the nodes.

Store all the addresses of nodes in LL headA.

Start traversing the LL headB, if current node's addr is found in hashSet, we can say that we got the current node as intersection.

If treversing reaches the NULL, means there is no interection, as if it was present then it should have found in HashSet.

```cpp
node* intersectionPresent(node* head1, node* head2) {
    unordered_set<node*> st;  // Set to store visited nodes from the first list
    while (head1 != NULL) {
        st.insert(head1);  // Insert nodes of the first list into the set
        head1 = head1->next;
    }
    while (head2 != NULL) {
        if (st.find(head2) != st.end()) return head2;  // If node is found in set, it's the intersection point
        head2 = head2->next;
    }
    return NULL;  // Return NULL if no intersection is found
}
```

**TC=O(m+n) as each LL is traversed once, and SC=O(N)**

## Optimal solution (Using two pointers to traverse, if they meet, we got solution)

Point the d1 to head of LL1 which is headA, and point d2 to head of LL2 which is headB.

Now start iterating the LL, move both by one step. While d1 != d2

If anyone becomes NULL, point them to the head of the opposite lists and continue iterating until they collide.

If there exists an intersection, then it would have found by d1==d2.

If there is no intersection then both d1 and d2 points to NULL making d1==d2 and ending the LOOP.

<img width="1465" height="832" alt="ezgif-571964899f6e4a7a" src="https://github.com/user-attachments/assets/05b8c802-7b00-4099-be55-8930fe84dff5" />
