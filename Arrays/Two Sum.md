# Two Sum

[LeetCode](https://leetcode.com/problems/two-sum/)

Return 2 indices (i,j) from array, whose sum of eles at that positions is Equal to Target

You assume that each input would have **exactly one solution** , and you may not use the same element twice.

You start to iterate whole array with i, and iterate i+1 to n-1 with j, creating combination of (i,j) as

```
n=4
(i,j) =>
(0,1)
(0,2)
(0,3)
(1,2)
(1,3)
(2,3)

And each time you match sum of values at that indices and value of target (arr[i]+arr[j])== target
```

CODE:

```
class Solution {
public:
    vector<int> twoSum(vector<int>& arr, int target) {
        int n = arr.size();
        for( int i=0;i<n;i++){
            for(int j=i+1;j<n;j++){
                if((arr[i]+arr[j])== target){
                    return {i,j};
                }
            }
        }
        return {};
    }
};
```
