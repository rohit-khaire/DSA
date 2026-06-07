# Trapping Rainwater

Given an array of non-negative integers representation elevation of ground. Your task is to find the water that can be trapped after rain .

[LeetCode](https://leetcode.com/problems/trapping-rain-water/)

**Easy Concept**

## Brute Force having 2 extra arrays for prefixMax and suffixMax

**waterCanBeTrapped = mix(leftMax,rightMax) - arr[i]**

As the smaller bar is the level till which water can be stored and it cannot go above it as this will lead to water overflow from smaller bar side instead of trapping

So it can store **MinimumBar-CurrentBar** level of Water

To find how much water can be trapped on top of each bar, you need to know the highest bar on the left and the highest bar on the right of that position. The water trapped depends on the smaller of these two heights minus the height of the current bar. If the current bar is taller than both sides, no water can be trapped there. This needs to be done for every bar in the array.
<br>
- Create prefixMax and suffixMax array
- Traverse entire OG array from left, for each bar in OG Array, look for max found till now and store it in prefixMax array, for oth index it's max is arr[0], for ith index it's prefixMax is max(prefixMax[i-1],arr[i])
- Traverse entire OG array from right to left, for each bar in OG Array, look for max found till now and store it in suffixMax
<img width="588" height="286" alt="image" src="https://github.com/user-attachments/assets/3f025a5f-cf48-4f8d-9d50-434de2463884" />

- For each bar in OG array,Calculate the trapped water on the current bar as ``min(maxLeft, maxRight) - current height``.
- Sum all trapped water from each bar to get the total amount of trapped water.

Logic:
Someone who is biggest in right help, as in between blocks are smaller than it, so there is no one to stop(greater than suffixMax) inbetween current bar and that tallest bar of right

Smaller limits the trapped water, going above it causes overflow

<img width="427" height="402" alt="image" src="https://github.com/user-attachments/assets/2ae5bb40-b46d-48ea-a77b-d72bab3c0a4f" />

<br><br>
<img width="447" height="206" alt="image" src="https://github.com/user-attachments/assets/9d89e258-48c2-4c31-9378-272401584d74" />

**TC=O(N) for creating prefixMax + O(N) for creating suffixMax + O(N) for calculating water trap = O(3N)**

**SC=O(2N) as prefixMax and suffixMax are extra space used**

<br><br><br>

# OPTIMAL using Two pointers one at 0th and another at n-1th

leftIndex-> &nbsp;&nbsp;&nbsp;&nbsp; <-rightIndex

**I always choose minimum from left and right vals, this means I got support of that max bar(opposite of min), Now I check if that minimum value is less thann leftMax/rightMax?**
  - If yes, then I can trap water
  - Not, means I am bigger than leftMax/rightMax, I can be problem for further trapping, so now I am the new *leftMax/rightMax*
Move further

Steps:

We point to 0th and last index of Array

We can move till our left and right index becomes equal (left goes in right direction [left++] and right goes in left direction [right--] ) 

Algorithm:
1) Compare values at left and right indices,we choose the minimum value
> In case of left and right values are equal, we are choosing left value
2) Is that chosen value less than leftMax(if left value is chosen) ? 
  • Yes, then add difference of left Value and leftMax to Total
  • No, means chosen value is our new max, so make it leftMax
> If chosen value is right, then same steps with rightMax
3) Move pointer to next (if chosen value is left then left++, else right--) 
4) Repeat 1,2,3 till left becomes equal to right
5) Finally return the Total
<img width="490" height="325" alt="image" src="https://github.com/user-attachments/assets/05660fa1-5ef7-40f3-ab51-3df0362009b7" />

**The index at which your leftIndex becomes equals to rightIndex is the highest bar in the array**
<br>
```cpp
class Solution {
public:
    int trap(vector<int>& arr) {
        int n=arr.size();
        if(n==1) return 0;
        int total=0,leftMax=0,rightMax=0;
        int leftIndex=0;
        int rightIndex =n-1;
        while(leftIndex<rightIndex){ //When rightIndex==leftIndex, that is max height of whole array
            //Go with smaller height
            if(arr[leftIndex]<=arr[rightIndex]){ //We go with smaller,which is left height
                if(arr[leftIndex]<leftMax){ //If leftMax is more than me, then only I can store
                    total+= leftMax-arr[leftIndex];
                }else{
                    leftMax=arr[leftIndex];
                }
                leftIndex++;
            }else{
                //arr[leftIndex]>arr[rightIndex], we go with smaller, which is right height
                if(arr[rightIndex]<rightMax){ //I can only store when I am smaller than rightMax
                    total+= rightMax-arr[rightIndex];
                }else{
                    rightMax=arr[rightIndex];
                }
                rightIndex--;
            }
        }
        return total;
    }
};
```

**TC=O(N) and SC=O(1)**
