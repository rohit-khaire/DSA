# Container with Most Water

[Leetcode](https://leetcode.com/problems/container-with-most-water/description/)

Find the maximum unit of water (Area) you can store in Container

We want maximum water which we can store,.

# Approach - Two pointers

- We just point left to 0 and right to N-1
- Now we start a loop while(left<=right)
  - calculate the water we can store in the container which has 2 ends left & right
  - we can calculate it by (right-left) which gives length of container, now we need lower height from left and right
  - area = length * height
  - If this area is > max, then store it
  - If left height is smaller or == to right height, we move left ahead
  - else move right one step back

```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int maxi =0;
        int left=0;
        int right=height.size()-1;
        while(left<=right){
            int area = (right-left) * min(height[left],height[right]);
            maxi=max(maxi,area);
            if(height[left]<=height[right]) left++;
            else right--;
        }
        return maxi;
    }
};
```
