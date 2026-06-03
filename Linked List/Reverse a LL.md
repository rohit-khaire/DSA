# Reverse a LL

Problem Statement: Given the head of a singly linked list, write a program to reverse the linked list, and return the head pointer to the reversed list.

[LeetCode]()

## Brute Force using Stack

Use a stack to store all the eles of LL, then again start iterating the LL and replace the eles of LL with STACK eles

1. Traverse and put all eles in STACK
2. Traverse and replace all the eles by STACK eles

```cpp
temp = head;
stack st;
while(temp!=NULL){
  st.push(temp->data);
  temp=temp->next;
}
temp=head;
while(temp!=NULL){
  temp->value=st.top();
  st.pop()
  temp=temp->next;
}
```

**TC=O(2N) and SC=O(N)**

## OPTIMAL using Pointers and without extra space

prev  &emsp;   temp   &emsp;  front

We have 3 pointers, temp is current node and prev means previous node and front means the Node after current/temp Node

make Current/Temp -> next = prev

Then move ahead by prev=temp, temp=front and front=temp->next


```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode *temp = head;
        ListNode *prev = NULL;
        while(temp!=NULL){
            ListNode *front = temp->next;
            temp->next = prev;
            prev=temp;
            temp=front;
        }
        return prev;
    }
};
```


**TC=O(N) and SC=O(1)**

## Recursive SOlution

<img width="287" height="110" alt="image" src="https://github.com/user-attachments/assets/df8c5e38-fd5e-43bc-9b5b-9ba555a8b564" />

The function ``reverseList`` returns newHead by reversing the the List. If current element is NULL or current cha Next is NULL then it's already in reversed order. We can access the last element of reversed list by using the current cha next pointer.

```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* curr) {
        if(curr==NULL || curr->next==NULL){
            return curr;
        }
        ListNode *newHead=reverseList(curr->next);
        ListNode *lastEleOfReversed=curr->next;
        lastEleOfReversed->next=curr;
        curr->next=NULL;
        return newHead;

    }
};
```

<img width="736" height="327" alt="image" src="https://github.com/user-attachments/assets/da61ee41-12f0-4cd8-a87d-6041862a4ad3" />

Time Complexity: O(n),Each node is visited exactly once during the recursive call, and we do constant-time work for each node (like flipping pointers).

Space Complexity: O(n),The recursion stack goes up to n levels deep (one for each node), which uses extra space on the call stack.
