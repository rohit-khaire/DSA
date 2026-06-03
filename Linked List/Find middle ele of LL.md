# Find middle ele of LL

[LeetCode](https://leetcode.com/problems/middle-of-the-linked-list/description/)

## Brute Force

Traverse the LL and get the count for NO. of elements in the LL

Now get count/2 to get the mid

Now again start iterating the LL and also have count of it, and get the mid element when cnt==(length/2)

**TC=O(N+(N/2))=O(N) and Space Complexity : O(1)**


## OPTIMAL using Tortoise and Hare Algorithm

Can also use it find the loop in the LL

```cpp
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        if(head==NULL || head->next==NULL) return head;
        ListNode *slow=head;
        ListNode *fast=head;
        while(fast!=NULL && fast->next!=NULL){
            slow=slow->next;
            fast=fast->next->next;
        }
        return slow;

    }
};
```

<img width="432" height="193" alt="image" src="https://github.com/user-attachments/assets/7d1256b1-3c08-4742-8860-2628340d7fa4" />

<img width="823" height="514" alt="image" src="https://github.com/user-attachments/assets/2f9b678b-7e97-44fb-8945-106f89731175" />



Time Complexity: O(N/2) The algorithm requires the 'fast' pointer to reach the end of the list which it does after approximately N/2 iterations (where N is the total number of nodes). Therefore, the maximum number of iterations needed to find the middle node is proportional to the number of nodes in the list, making the time complexity linear, or O(N/2) ~ O(N).

Space Complexity : O(1) There is constant space complexity because it uses a constant amount of extra space regardless of the size of the linked list. We only use a few variables to keep track of the middle position and traverse the list, and the memory required for these variables does not depend on the size of the list.
