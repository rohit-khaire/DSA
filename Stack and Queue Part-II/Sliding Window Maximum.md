# Sliding Window Maximum

[LeetCode](https://leetcode.com/problems/sliding-window-maximum/)

Given an array of integers arr, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position. Return the max in each sliding window.

## Brute Force

Brute Force (Sliding Window Maximum)
1. Take every window of size K from left to right (0 to N-K).
2. Traverse all K elements inside the current window and find the maximum.
3. Store the maximum in the answer array and move the window by one position.

Complexity:
- TC = O((N-K+1) × K) ≈ O(NK)
- SC = O(1) (excluding output array)

# Approach, Very Simple, Solved it in first attempt just by understanding the Concept

As our window is sliding, we can have a Queue to add element from back and remove element from front to maintain a k size Window

We require maximum element from the Window, so we can think of Monotonic Stack having decreasing order from left to right, and we can add elements to it from left

This horizontal decreasing oder from left to right ensures we have next greater element if our greatest element gets pop due to sliding of Window

As we are maintaining a monotonic horizontal stack where insertion is from left, we can remove the elements from left which are smaller than the current nums[i], so that we end up just after the bigger element maintaining a decreasing order

Ex. Stack=> [9,8,4,3] when our window slides, firstly we remove expired element from front to maintain k size, so 

new stack => [8,4,3] and we encounter 6, so we remove all the smaller elements from back and then add it

Final Stack => [8,6]

Can we have Queue(To add from back and remove from front) and Monotonic Stack(insert from back/right and remove from right/back) together?

=> front=pop() and back=push(),pop()

**Yes, we can use a Double Ended Queue (deque)**

It provides, push() and pop() from both the ends front() and back()

Now we are using **Deque** and we will be storing indices to elements rather than value,, so that we can know that which element is expired now (i-k)

We can traverse the Array in O(N), each element only once

- Initialize a deque and We start traversing the array from 0 to N-1 _O(N)_
- We encounter i th element, fisrtly if deque is not empty, then remove the expired index from Deque's front() (To know expired: i-k)
- Then we remove all the smaller elements from back of deque (Elements which cannot be potential maximum, as I am(nums[i]) greater than them)
- Push the current element from back
- If our i is on k-1 th index(1st window) or further then only we can store the result
  - The current window's maximum is Deque's front
 
Deque always remains in decreasing order like: [9,8,7,6,5]


```cpp
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        deque<int> dq; //Store indices of potential maximums, store in decreasing order of vals
        //So that even front gets removed cause of window sliding, then second max remains
        // While slidings, push from back and pop from front
        // To maintain monotonic stack/order, remove from back while back() is smaller than current
        vector<int> ans;
        for(int i=0;i<nums.size();i++){
            if(!dq.empty() && dq.front()<=i-k){ //remove expired index
                    dq.pop_front();
            }
            while(!dq.empty() && nums[dq.back()]<=nums[i]){ //remove weaker elements
                dq.pop_back();
            }
            dq.push_back(i); //push current element
            if(i>=k-1){    
                ans.push_back(nums[dq.front()]);
            }
        }
        return ans;
    }
};
```

TC=O(N) and SC=O(N-K) ans array
