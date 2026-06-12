# LRU Cache

Least Recently Used Cache, remove the one which is not recently used and add the new

Capacity shows Maximum No. of {Key,Val} pairs we can have in LRU, get returns val coresponding to key, if key is not there in LRU Cache the return -1

_put_ is used to add {key,val} pair to LRU 

# Approach

Using Doubly LL and Map<key,*Node> for hashing

Have dummy head whose next pointing to dummy tail and prev pointing to NULL

Have dummy tail whose next pointing to NULL and prev pointing to dummy head

**Prev of Dummy Tail is LRU**

When _put_ is called, check if that key is present in DLL, can get it from map

If it's not present in map, then insert it in DLL from front, else if it's present in map, then access it(Node) and update it's val and grab it to front

While inserting new Nodes, insert new nodes between dummy Head and Dummy Tail, treat insertion as insertFront like a Queue[Insertion from front and deletion from end]  (but between dummy head and dummy tail)

If capacity is full then we insert the Node at front and delete the Last Node (Prev of Dummy Tail Node)

When _get_ is called, check if that val exists in the DLL, by finding it in map

  - If it exists, access that Node and return the value, and remember to grab that Node and bring(insert) it in front (Reuse the Nodes, So that you don't need to update the map)
  - If it not exists then return the -1



