# Delete Node in a Linked List

[LeetCode](https://leetcode.com/problems/delete-node-in-a-linked-list/description/)

Problem Statement: Write a function to delete a node in a singly linked list. You will not be given access to the head of the list instead, you will be given access to the node to be deleted directly. It is guaranteed that the node to be deleted is not a tail node in the list.


# OPTIMAL SOLUTION ONLY:

As you are given the current node which is to be deleted, so you can just copy the elements (val and next) of next Node (current->next)

Now you have 2 duplicate nodes and both are pointing to the same next location, and thus the current node is deleted

<img width="556" height="322" alt="image" src="https://github.com/user-attachments/assets/705edafc-0586-43a9-8611-552dcce7bbde" />

```cpp
class Solution {
public:
    void deleteNode(ListNode* node) {
        node->val=node->next->val;
        node->next=node->next->next;
    }
};
```

**TC=O(1) and SC=O(1)**
