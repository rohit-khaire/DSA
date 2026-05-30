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

