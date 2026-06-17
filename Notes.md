# Simple Notes/funcs/commands

1D vector: vector<int> arr(n,-1);  // size n and initialized by -1

2D vector: 

vector<vector<int>> arr;

vector<vector<int>> dp(m, vector<int>(n, -1));  //m*n matrix with -1 vals

v[0].first;  //access 0th row cha 0th ele

v[0].second;  // access 0th row cha 1th ele *Can also use with pair: vector<pair<int,int>> v; or pair<int,int> p;*

reverse(A.begin(), A.end())   {Excluding 2nd parameter wala index like range() }

sort(A.begin()+ 2, A.end() ) <br>

N = A.size()    (Total no. of ele in 1D) <br>

In 2D Array:

To get no. of rows: a.size();

To get no. of cols : arr[0].size()

swap( A[i], A[ind] )

min( __ , __ )

max( __ , __ )

return empty array: {}

 return array with 2 elements: { i, j }

 Check two arrays are same => A == B

 check if variable is integer or not => more >= INT_MIN && more <= INT_MAX

 Pass by reference for Vector => 
 
 ```
void rotate( vector<int> &arr){}

```
<br> 

- v.empty();  => check empty

- v.back(); => returns last element (In 2D Vector, get last row)

- v.push_back(x);  => insert, can also add whole row at last `ans.push_back(arr[i])`


Variable sized array Declaration using Vector:

``vector<int> hash((n * n) + 1, 0);``


MAP:

ordered map => map<int,int> mpp;    // ordered by keys // TC = logn per operation

unordered map => unordered_map<int,int> mpp;  // average TC= O(1) and worst is O(N) per operation

To store element in map => mpp[0] = 5; => {0,5}  // BY default values are initially 0s

mpp.find(7) => searches for key 7

It returns an iterator.

When found: points to 7

If not found: it points to end of map, mpp.end()

Why not if(mpp[more]) used, as if more not found, then it creates a one with 0 as value

<br>

To make any -ve no. positive = abs(x) or -1*x

**Use set to avoid duplicates**

set<int> st;    //set if integers

set<vector<int>> st;  // set of int vector

st.insert({arr[i], arr[j], arr[k], arr[l]});  //insert vector in set

vector<vector<int>>(st.begin(), st.end());  // Convert set of vectors To vector of int vector

**Use long long to compute huge numbers calculations**

temp.count(more)  // get the count from set

### `set` in C++ — Quick 1-Line Notes

* `set<int> s;` → Stores **unique elements in sorted order** (ascending by default).
* `s.insert(x);` → Inserts `x` if not already present. **O(log n)**.
* `s.erase(x);` → Removes `x` from the set. **O(log n)**.
* `s.count(x);` → Returns `1` if `x` exists, otherwise `0`. **O(log n)**.
* `s.find(x);` → Returns iterator to `x`, or `s.end()` if not found. **O(log n)**.
* `s.size();` → Returns number of elements. **O(1)**.
* `s.empty();` → Returns `true` if set is empty. **O(1)**.
* `s.clear();` → Removes all elements.
* `s.begin();` → Iterator to the smallest element.
* `s.rbegin();` → Reverse iterator to the largest element.
* `*s.begin();` → Smallest element in the set.
* `*s.rbegin();` → Largest element in the set.
* `s.lower_bound(x);` → First element **≥ x**. **O(log n)**.
* `s.upper_bound(x);` → First element **> x**. **O(log n)**.
* `distance(s.begin(), s.find(x));` → Index-like position of `x` (costly: **O(n)**).
* `set<int, greater<int>> s;` → Stores unique elements in descending order.

### Common Checks

```cpp
if(s.count(x))      // x exists
if(s.find(x)!=s.end()) // x exists
```

### Iteration

```cpp
for(auto it : s) cout << it << " ";
```


* **Ordered Set (`set`)** → Implemented using **Red-Black Tree (BST)**, so **insert, erase, find, count = O(log n)**


* **Unordered Set (`unordered_set`)** → Implemented using **Hash Table**, so **insert, erase, find, count = O(1) average, O(n) worst case**.


* `set` → **Sorted + Unique + O(log n)**
* `unordered_set` → **Unsorted + Unique + O(1) average** 



# String

s.substr(position/index,length)   to get substring from a string ``s`` and position is starting index and length is length of substring, if grater length then I think it gives whole string
