# Palindrome LL

Solved perfectly in first attempt without looking at the solution

Given the head of a singly linked list, return true if it is a palindrome or false otherwise.

[LeetCode](https://leetcode.com/problems/palindrome-linked-list/description/)

# Solution is Also Explained in DSA Notebook

## Brute Force

Have A stack, point temp to Head of LL and start pushing elements of LL into the Stack

When temp becomes Null, point it to head again

Now start traversing all elements of LL and compare it with top of stack and pop it from stack

**TC=O(N+N = 2N) and SC=O(N)**

## Better 

- Have a vector and store elements(vals) of LL in the vector (push_back vals of LL into the vector)
- Now start applying palindrome logic on the vector
- get last as arr.size()-1 and start as arr[0]
- start iterating as start++ and last--
- Compare the start and last, if they miss match then return false

```cpp
class Solution {
public:
    bool isPalindrome(ListNode* head) {
      vector<int> arr;
      while(head){
        arr.push_back(head->val);
        head=head->next;
      }
      int i=0, j=arr.size()-1;

      while(i<j){
        if(arr[i] != arr[j]){
            return false;
        }
        i++;
        j--;
      }
        return true;
    }
};
```

**TC=O(N+(N/2)) and SC=O(N)**

# OPTIMAL SOLUTION

- Get the mid of the LL using Tortoise and Hare method ( slow and fast pointers )
- Cases to stop:
  - Even Length of LL: stop when fast->next->next == NULL, so that slow points to N/2 th position
  - Odd Length of LL: stop when fast->next==NULL, so that slow points to Exact mid position of LL
- Revserse the LL from ``slow->next``
- We obtain a newHead by reversing the LL from slow->next, this newHead is pointing to last Node of LL
- Now slow->next Node's next is pointing to NULL
- Now point ``temp1`` to head and ``temp2`` to newHead
- Start comparing temp1 and temp2 vals
  - If miss match occurs, again bring back the LL to original state by reversing slow->next, and return ``false``
- Move temp1 and temp2 each while temp2!= NULL
- If temp2 reaches NULL, means all elements of LL are checked and now we can return true
> Remember to bring back the LL to it's original state before returning


```cpp
class Solution {
public:
    ListNode* reverse(ListNode *head){
        if(head==NULL || head->next==NULL) return head;
        ListNode *newHead = reverse(head->next);
        head->next->next=head;  //It was pointing to NULL
        head->next=NULL;
        return newHead;
    }
    bool isPalindrome(ListNode* head) {
        if(head==NULL || head->next==NULL) return true;
        ListNode *slow=head;
        ListNode *fast=head;
        while(fast->next!=NULL && fast->next->next!=NULL){
            slow=slow->next;
            fast=fast->next->next;
        }
        ListNode *newHead = reverse(slow->next);
        ListNode *temp1 = head;
        ListNode *temp2 = newHead;
        while(temp2!=NULL){
            if(temp1->val != temp2->val){
                reverse(newHead);
                return false;
            }
            temp1=temp1->next;
            temp2=temp2->next;
        }
        reverse(newHead);
        return true;
    }
};
```



| Operation                              | Nodes Processed | TC   |
| -------------------------------------- | --------------- | ---- |
| Find middle using slow & fast pointers | N               | O(N) |
| Reverse second half                    | N/2             | O(N) |
| Compare first and second halves        | N/2             | O(N) |
| Restore second half (reverse again)    | N/2             | O(N) |

**TC=O(N) and SC=O(N/2 + N/2 = N)**
