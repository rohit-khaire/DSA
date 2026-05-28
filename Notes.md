# Simple Notes/funcs/commands

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

ordered map => map<int,int> mpp;    // ordered by keys

unordered map => unordered_map<int,int> mpp;

To store element in map => mpp[0] = 5; => {0,5}  // BY default values are initially 0s

<br>

To make any -ve no. positive = abs(x) or -1*x

