# Linked List Cycle

Detect the cycle in the LL and return true or false

[LeetCode](https://leetcode.com/problems/linked-list-cycle/description/)

## Brute Force using Hashing

Use a map to store whole node (Val,NextAddr) 

Always check if that Node is already appeared or not, if yes It means it's a Cycle

If same element is not in Map then add it to map, so that later it can be found

If We reach end of LL (NULL) return false, there is no cycle

```cpp
    bool detectLoop(Node* head) {
        // Initialize a pointer at head
        Node* temp = head;

        // Create a map to keep track of visited nodes
        unordered_map<Node*, int> nodeMap;

        // Traverse the linked list
        while (temp != nullptr) {
            // If node already exists in map, loop detected
            if (nodeMap.find(temp) != nodeMap.end()) {
                return true;
            }
            // Store the current node in the map
            nodeMap[temp] = 1;

            // Move to the next node
            temp = temp->next;
        }

        // If traversal completes, no loop detected
        return false;
    }
```

Time Complexity: O(N*LogN), we traverse the entire linked list once and store and retrieve nodes from the hash map. Map operations have a worst time space complexiy of O(LogN).

Space Complexity: O(N) , additional amount of extra space is used to store nodes in a hash map.


# OPTIMAL using Floyd's Cycle Detection

If head is NULL or if head->next is NULL then it means there is no cycle

Point slow and fast to the Head of LL

Now start traversing the LL until NULL (end) of LL is faced

Move slow by 1 Node and Fast by 2 Nodes

If NULL is faced then it means there is no Cycle

If there is cycle, then There will be a node at which slow==fast



```cpp
class Solution {
public:
    bool hasCycle(ListNode *head) {
        ListNode* slow=head;
        ListNode* fast= head;
    if(fast==NULL) return false;
        while(fast!=NULL && fast->next!=NULL){

            slow = slow -> next;
            fast = fast->next->next;

            if(slow == fast) return true;
        }
        return false;
    }
};
```

*This is only for detection, but if you want the entry of cycle then it can be found using moving slow to head and now moving slow and fast both by 1 nodes*

**Time Complexity: O(N), we traverse the entire linked list once. The fast pointer either reaches the end of the list or meets the slow pointer in linear time.**

**Space Complexity: O(1) , constant amount of extra space is used detect a cycle using Floyd's Cycle Detection Algorithm.**
