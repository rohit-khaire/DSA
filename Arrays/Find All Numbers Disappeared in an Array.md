# Find All Numbers Disappeared in an Array

[LeetCode](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/)

Given an Array ``nums`` of size of N 

This array contains elements only between range [1,N] including 1 and N

For example, nums = [4,3,2,7,8,2,3,1]

We can see that when any number is missing, to fill it's absence any other number from [1 to N] takes it's position

So there maybe times where a number is repeated in Nums


# Approach - Without Hash, TC:O(2N) and SC:O(1)

- Get N = nums.size()
- start checking each number in nums array
  - we can mark a number as visited by making element at that index-1 as negative, as we know that every number is positive initially as it ranges from 1 to N
  - Maybe current nums[i] can be negative, hence take abs(nums[i]), get required index as abs(nums[i])-1 (This can make 1 to N range as 0 to N-1 range)
  - we got required index = abs(nums[i])-1
  - now if element at that index is already negative, it means nums[i] is repeating
    - Don't do anything
  - else make it negative
- Create an Array to store result, vector<int> res;
- now start traversing nums array again
  - if nums[i] is positive, it means index ``i`` was missing, hence nums[i] is not negative
    - Add it in result array
  - else move formward
- return result

```cpp
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
        int n = nums.size();
        for(int i=0;i<n;i++){ //nums[i]= {1 to N}, N index doesn't exist, and 1 can be represented on index 0
            //All nums[i] are positives initially; when we have nums[i] we make element at index abs(nums[i])-1 as negative; if nums[i] is negative, we make abs(nums[i])-1 as negative
            int index = abs(nums[i])-1;
            if(nums[index]>0){
                nums[index] = -nums[index];
            }
        }
        //Now numbers which appeared are made as negative, so positive numbers are missing ones
        vector<int> res;
        for(int i=0;i<n;i++){
            if(nums[i]>0){
                res.push_back(i+1);
            }
        }
        return res;
    }
};
```

TC:O(2N) and SC:O(1)
