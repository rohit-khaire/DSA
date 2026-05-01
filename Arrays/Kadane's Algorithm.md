# Kadane's Algo - Maximum Subarray

[LeetCode Link](https://leetcode.com/problems/maximum-subarray/description/)

arr[]= {-2,3,4,5}

Subarray = Continous vals {3,4,5}

SubSequence = Can be random {-2,4,5}


Example of SubArray:

arr[]={-2,-3,4,-1}

{-2,-3} 

{-2,-3,4}

{-2,-3,4,-1}

{-3,4}

{-3,4,-1}

{4,-1}


## Brute Force

```
maxm= INT_MIN;
for(i=0;i<n;i++){
  for(j=i;j<n;j++){
    sum=0;
    for(k= i->j){
      sum+=arr[k];
    }
    maxm= max(sum,maxm)
  }
}
```

**TC approx O(N^3)**

**SC is O(1)**

## Better

Don't calculate sum with loop, just remember previous sum and add current value in it.

So it will remove 1 loop (i.e. k=i->j)

**TC will be O(N^2)**

**SC will be O(1)**


## OPTIMAL SOLUTION

**Kadane's Algo**

Iterate once and keep adding arr[i] in sum, and if my sum is < 0 then make it 0 and drop it. 


Given an integer array nums, find the subarray with the largest sum, and return its sum.


```
class Solution {
public:
    int maxSubArray(vector<int>& arr) {
        int n = arr.size();
        int sum=0;
        int maxm=INT_MIN;
        for(int i=0;i<n;i++){
            sum+=arr[i];
            if(sum>maxm){
                maxm=sum;
            }
            if(sum<0){
                sum=0; // Do not carry any negative sum to future
            }

        }
        return maxm;
    }
};
```

**TC is ON and SC is O(1)**


### Now Provide me subarray which gave u maxm sum



sum=0

tempStart=0

start=0 // used to return starting index of result

end=0  // used to teturn end index of result

maxm=INT_MIN

**sum+arr[i] -> sum>maxm => new max & start=tempStart & end=i -> sum<0 => sum=0 & tempStart=i+1**


### Dry Run Table (Kadane with Indices)

Array: {-2, -3, 4, -1, -2, 1, 5, -3}

| i | arr[i] | sum (after add) | maxm | tempStart | start | end |
|---|--------|-----------------|------|-----------|-------|-----|
| 0 | -2     | -2              | -2   | 0         | 0     | 0   |
|   |        | sum < 0 → 0     |      | 1         |       |     |
| 1 | -3     | -3              | -2   | 1         | 0     | 0   |
|   |        | sum < 0 → 0     |      | 2         |       |     |
| 2 | 4      | 4               | 4    | 2         | 2     | 2   |
| 3 | -1     | 3               | 4    | 2         | 2     | 2   |
| 4 | -2     | 1               | 4    | 2         | 2     | 2   |
| 5 | 1      | 2               | 4    | 2         | 2     | 2   |
| 6 | 5      | 7               | 7    | 2         | 2     | 6   |
| 7 | -3     | 4               | 7    | 2         | 2     | 6   |


*Final Result*

Max Sum = 7

Start Index = 2

End Index = 6

Subarray = {4, -1, -2, 1, 5}



```
class Solution {
public:
    vector<int> maxSubArray(vector<int>& arr) {
        int n = arr.size();
        
        int sum = 0;
        int maxm = INT_MIN;
        
        int start = 0, end = 0;
        int tempStart = 0;

        for(int i = 0; i < n; i++) {
            sum += arr[i];

            if(sum > maxm) {
                maxm = sum;
                start = tempStart;
                end = i;
            }

            if(sum < 0) {
                sum = 0;
                tempStart = i + 1; // next element could be new start
            }
        }

        return {start, end}; // returning indices
    }
};
```



