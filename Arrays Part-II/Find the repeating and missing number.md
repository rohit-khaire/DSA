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
