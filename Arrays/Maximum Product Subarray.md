# Max Product Subarray

subarray must be contiguous. We need to return the maximum possible product of a subarray

[Leetcode](https://leetcode.com/problems/maximum-product-subarray/)

# Approach

We keep track of maxProduct and minProduct as one negative number can make min->max

- We point maxProduct and minProduct to nums[0] and currently our answer is also nums[0]
- We start a for loop from i=1 to <n
  - We get newMaximum from {nums[i], minProd*nums[i], maxProd*nums[i]} as if nums[i] is max from others means our new subarray starts from here
  - We get newMinimum from same elements
  - Now our ans is max(ans,newMaximum)
  - and we then set maxProd=newMaximum and minProd=newMinimum
- return ans

```cpp
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int n = nums.size();
        int ans = nums[0];
        int minProd = nums[0];
        int maxProd = nums[0];
        for(int i=1;i<n;i++){
            //Possible products: 1) Itself only nums[i]  2) minProd*nums[i]  3)maxProd*nums[i]
            int newMax = max({nums[i],minProd*nums[i],maxProd*nums[i]}); //storing in new variable as we require maxProd further
            int newMin = min({nums[i],minProd*nums[i],maxProd*nums[i]});
            ans = max(ans,newMax); //As when new subarray start, maybe prev subarray has prod>currentSubArray
            maxProd=newMax;
            minProd=newMin;

        }
        return ans;
    }
};
```

TC:O(N) & SC:(1)
