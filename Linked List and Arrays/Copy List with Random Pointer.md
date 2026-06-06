# Copy List with Random Pointer

A linked list of length n is given such that each node contains an additional random pointer, which could point to any node in the list, or null.

Create a *deep copy* of this LL where each Node contains ``val,next,random``

deep copy means fully separate copy, any changes in copy should not affect the original and vice versa.

**Deep Copy:** Creates entirely new nodes with the same values and connections as the original list, so modifying the original list does not affect the copied list and vice versa. 

[LeetCode](https://leetcode.com/problems/copy-list-with-random-pointer/description/)

# Solved optimal solution in first time, just by understanding the 3 steps of traversing

## Brute Force using HashMap

Use hash map to store <Node,Node> as {OriginalNode,CopyNode}

Traverse the LL, and for each Node create a copy Node, and store that OG Node and it's copy (only value copied till now) in Map

Now again start Traversing the LL, and now for each Node of OG LL, there is next and random, and both of these will now be having copy node as values and OG Node as Key

So using this, creating linkings like, for copy of Node 1{val of Node1 in Map}, point Copied Node's next to OG Node's next's dummy(val) in Map

DO same for random linking

**TC=O(2N) and SC=O(N) , as map stores all nodes**

## OPTIMAL SOLUTION 

Create a dummy for current Node with same val only-> Point current Node to dummy Node and dummy's next to current's next

So that Each Node points to their dummy and dummy points to next node of current

Now point current/temp again to Head and now 

-> Create Random linkings for dummy Nodes (OG's next are dummy, so OG's random's next is dummy's random)

-> Again point temp to head and now create linking of next

**TC=O(3N) and SC=O(1)**

> 1. Traverse and create dummy next to OG
> 2. Traverse and create Random linkings of dummy
> 3. Traverse and create ``next`` linkings of dummy


```cpp
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;
    
    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};
*/

class Solution {
public:
    Node* copyRandomList(Node* head) {
        if(head==NULL) return head;
        Node *temp= head;
        while(temp){ //Insert new dummy Nodes after each Node
            Node *newNode = new Node(temp->val);
            newNode->next=temp->next;
            temp->next=newNode;
            temp= newNode->next;
        }
        temp=head;
        while(temp){  //Random linking

            temp->next->random=(temp->random!=NULL)?temp->random->next:NULL;
            temp=temp->next->next;
        }
        Node *newHead = head->next;
        temp=head;
        while(temp){
            Node *res=temp->next;
            temp->next=res->next;
            res->next=(res->next!=NULL)?res->next->next:NULL;
            temp=temp->next;
        }
        return newHead;


    }
};
```

