# Find the repeating and missing number

[LeetCode](https://leetcode.com/problems/find-missing-and-repeated-values/description/)

## Extreme  Brute Force

Interate and get count of vals in Array. Whichever ele is having count as 0 is the missing number and the one having count as 2 is the repeating Number.


```
repeated, missing = -1
for(i=0 -> n-1){
  cnt=0;
  for(j=0 -> n-1){
    if(arr[j] == i ){ cnt++; }
  }
  if(cnt==0){ missing=i; }
  else if(cnt==2){ repeated=i; }
  if(repeated != -1 && missing!=-1) break;
}

```


TC = O(N^2)

SC = O(1)

## Use Hash ( Beats 100% )

Use hash => Create a new array and initialize all elements in it by 0s

Iterate through each element of Main Array, and increment the count stored in hash array by 1.

Now iterate the hash array and when ever count (value) appears as 2 is repeated value and 0 count represents missing value.

```
class Solution {
public:
    vector<int> findMissingAndRepeatedValues(vector<vector<int>>& grid) {
        int n = grid.size();
        // Value ranges from [1,n^2]
        vector<int> hash((n * n) + 1, 0);
        for(int i=0; i<n; i++){
            for(int j=0;j<n;j++){
                hash[grid[i][j]] +=1;
            }
        }
        int repeating = -1, missing=-1;
        for(int i=1;i< (n*n)+1;i++){
            if(hash[i]==2){
                repeating = i;
            }
            else if(hash[i]==0){
                missing=i;
            }
            if(repeating != -1 & missing != -1) break;
        }
        return {repeating, missing};
    }
};
```


*Create Variable sized Array using: vector<int> hash((n * n) + 1, 0)*

Vactor of size 0 -> (n*n) and all values set to 0.

**TC = O(n²) + O(n²) = O(2n²) = O(n²)**

Iteration on grid + Interation on Hash array

**SC = O(n²)**


## Optimal Solution to remove extra space

2 Ways : Maths and XOR

## Mathematical Optimal Solution

Where vals ranges for [1,n]

For A = {1,3,2,2}

repeated = 2

missing = 4

n = 4

We can get repeated and missing using maths

**Sum of N natural no. = n(n+1)/2**   = SN => 10

**Sum of squares of N natural no. = n(n+1)(2n+1)/6**   = S2N => 30

**Sum of A = 1+3+2+2 = 8**    = SA

**Sum of squares of vals of A = 1*1 + 3*3 + 2*2 + 2*2 = 1+9+4+4 = 18**  = S2A



SA-SN = {1+3+2+2} - {1+2+3+4} = 1+3+2+2  -1-2-3-4 = 2 -4 = **{repeating,missing} = {2,4}**

Now to get this in program:

SA - SN = -2  => X-Y=val1

S2A - S2N = 18 - 30 = -12  => X^2 - Y^2 = val2

X^2 - Y^2 = (X+Y)(X-Y) 

X+Y = val2/(X-Y) = val2/val1 => X+Y = val2


X,Y => <br>

X-Y = val1 <br>
X+Y = val2 <br>

Got X and Y , X is repeated and Y is missing value



