# 1299. Replace Elements with Greatest Element on Right Side

[Leetcode](https://leetcode.com/problems/replace-elements-with-greatest-element-on-right-side/description/)

For each element, replace current element with the maximum element in right subarray. For last element, replace it with -1


# Approach - Iterating from last and keeping track of maximum till now


- Have a variable maxi=-1, this variable stores maximum element found till now
- Start iterating from last index
  - Store current element in Temp variable
  - replace current element with maxi
  - Now store maxi=max(maxi,temp)

```cpp
class Solution {
public:
    vector<int> replaceElements(vector<int>& arr) {
        int maxi=-1;
        for(int i=arr.size()-1;i>=0;i--){
            int currentVal = arr[i];
            arr[i] = maxi;
            maxi = max(maxi,currentVal);
        }
        return arr;
    }
};
```

TC:O(N) & SC:O(1)

