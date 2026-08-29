# Squares of a Sorted Array

[Leetcode](https://leetcode.com/problems/squares-of-a-sorted-array/description/)

Given a list of Sorted, it contains negative numbers also. 

Example: -4,-2,0,1,3

Return a list containing Squares of these numbers, but result should be in Sorted manner

Example:

Input: nums = [-4,-1,0,3,10]

Output: [0,1,9,16,100]

# Approach - Two pointers, left and right, both moves to mid of Array

- Create a result Array of same size
- Have left pointer pointing to index 0
- Have right pointer pointing to index n-1
- now start filling the result array from right: loop from n-1 to 0
  - if(abs(nums[left]) >= abs(nums[right]))
    - store result[i] as nums[left]*nums[left]
    - left++
  - else
    - result[i] = nums[right]*nums[right]
    - right--
- return result

**Code:**

<br>

```cpp
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        int n = nums.size();
        int left =0;
        int right = n-1;
        vector<int> result(n);
        for(int i=n-1;i>=0;i--){
            if(abs(nums[left]) >= abs(nums[right])){ // can also directly compare squares: 
            //if (nums[left] * nums[left] >= nums[right] * nums[right])
                result[i] = nums[left] * nums[left];
                left++;
            }else{
                result[i] = nums[right] * nums[right];
                right--;
            }
        }
        return result;
    }
};
```

TC: O(N) and SC:O(N) as result array


