# LRU Cache

Least Recently Used Cache, remove the one which is not recently used and add the new

Capacity shows Maximum No. of {Key,Val} pairs we can have in LRU, get returns val coresponding to key, if key is not there in LRU Cache the return -1

_put_ is used to add {key,val} pair to LRU 

# Approach

Using Doubly LL and Map<key,*Node> for hashing

Have dummy head whose next pointing to dummy tail and prev pointing to NULL

Have dummy tail whose next pointing to NULL and prev pointing to dummy head

When _put_ is called, check if that key is present in DLL, can get it from map

If it's not present in map, then insert it in DLL, else if it's present in map, then access it(Node) and update it's val

While inserting new Nodes, insert new nodes between dummy Head and Dummy Tail, treat insertion as insertFront like a Queue (but between dummy head and dummy tail)

