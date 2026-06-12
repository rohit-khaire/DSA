# LRU Cache

[LeetCode](https://leetcode.com/problems/lru-cache/)

Least Recently Used Cache, when capacity becomes full, remove the one which is not recently used and add the new

Capacity shows Maximum No. of {Key,Val} pairs we can have in LRU, 
- get returns val coresponding to key, if key is not there in LRU Cache the return -1
- _put_ is used to add {key,val} pair to LRU 

# Approach

**Using Doubly LL and Map<key,*Node> for hashing**

Have dummy head whose next pointing to dummy tail and prev pointing to NULL

Have dummy tail whose next pointing to NULL and prev pointing to dummy head

**Prev Node of Dummy Tail is LRU** and **Dummy Head's next is MRU**

When _put_ is called, check if that key is present in DLL, can get it from map

If it's not present in map, then insert it in DLL from front, else if it's present in map, then access it(Node) and update it's val and grab it to front

While inserting new Nodes, insert new nodes between dummy Head and Dummy Tail, treat insertion as insertFront like a Queue[Insertion from front and deletion from end]  (but between dummy head and dummy tail)

If capacity is full then we insert the Node at front and delete the Last Node (Prev of Dummy Tail Node)

When _get_ is called, check if that val exists in the DLL, by finding it in map

  - If it exists, access that Node and return the value, and remember to grab that Node and bring(insert) it in front (Reuse the Nodes, So that you don't need to update the map)
  - If it not exists then return the -1

# Simple Idea, Solved it in 1st attempt, Very Very Easy, Just understand the concept

Capacity is maximum no. of nodes the DLL can have, We don't need any counter to keep track of capacity, we can get no. of nodes by size of map (mpp.size())

We use Doubly LL, At starting Dummy head points to Dummy Tail and vice versa, and our map is empty

**LRU** will be our Tail's prev & **MRU** will be our head's next

We define deleteNode function which deletes current node, and insertAfterHead() func which inserts the current node after Head

Insead of deleting the Node just create New linkings, and instead of creating new nodes everytime, just change the current node's key and value

Try to reuse the Nodes

> Insertion happens from front and deletion happens from last, whenever you access any node, bring it to front, so at the last you can have LRU

- get(key) , used to get the value of respective key
    - check if that key exists in the map?
      - No, then return -1
      - Yes, get it's Node address from Map, delete the Node(Just Delinking) and insertAfterHead() , so this node becomes _MRU_ , return it's value
-  put(key,value) , used to put the pair of {key,value} in LRU Cache, if capacity is already full before insertion of current pair, then remove LRU and add the current pair as _MRU_
  - Find if that key already exists in the map?
    - Yes, then get that Node's address and just update it's val and make it as _MRU_ by moving it to front(head's next)
    - No, then go ahead
  - You are here this means you are going to insert new Node in the Cache, Check if map.size()==capacity?
    - Yes, means LL is full, we need to remove LRU and insert the new pair as MRU
    - No, directlt insert new pair in front (head's next)

```cpp
class Node{  //Doubly LL Node
    public:
    int key,val;
    Node *prev, *next;
    Node(int _key,int _val){
        key=_key;
        val=_val;
        prev=NULL;
        next=NULL;
    }
};

void deleteNode(Node *curr){
    Node *previousNode = curr->prev;
    Node *nextNode = curr->next;
    previousNode->next = nextNode;
    nextNode->prev = previousNode;
}
void insertAfterHead(Node *head,Node *curr){
    curr->next=head->next;
    curr->prev=head;
    head->next->prev=curr;
    head->next=curr;
}

class LRUCache {
    unordered_map<int,Node*> mpp;
    Node *head,*tail;
    int cap;
public:
    LRUCache(int capacity) {
        cap=capacity;
        head = new Node(-1, -1);
        tail = new Node(-1,-1);
        head->prev=NULL;
        head->next=tail;
        tail->prev=head;
        tail->next=NULL;

    }
    
    int get(int key) {
        if(mpp.find(key)==mpp.end()) return -1;
        Node *temp = mpp[key];
        deleteNode(temp);
        insertAfterHead(head,temp);
        return temp->val;
    }
    
    void put(int key, int value) {
        if(cap==0) return; //handle edge case when capacity given is 0, so store nothing
        if(mpp.find(key)!=mpp.end()){
            Node *temp= mpp[key];
            temp->val = value;
            deleteNode(temp);
            insertAfterHead(head,temp);
            return;
        }
        if(mpp.size() == cap){
            Node *temp = tail->prev;
            mpp.erase(temp->key);
            deleteNode(temp);
            insertAfterHead(head,temp);
            temp->key=key;
            temp->val=value;
            mpp[key]=temp;
        }else{
            Node *temp = new Node(key,value);
            insertAfterHead(head,temp);
            mpp[key]=temp;
        }
    }
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```


| Operation         | Time Complexity  |
| ----------------- | ---------------- |
| `get(key)`        | **O(1)** average |
| `put(key, value)` | **O(1)** average |
| Space             | **O(capacity)**  |

SC=O(N) as DLL is of N size(=capacity) and Map is also of N size at max


If you write this in an interview and explain:

- Hash map for O(1) lookup
- Doubly linked list for O(1) delete/insert
- Head = MRU, Tail = LRU
- Node reuse optimization during eviction

that would be considered a fully optimal LRU Cache solution.
