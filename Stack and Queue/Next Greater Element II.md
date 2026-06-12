# Next Greater Element II

[LeetCode](https://leetcode.com/problems/next-greater-element-ii/)

We have to find first element which is greater than current element in the right side of current element (same as NGE I)

But here the array is circular, last ele's next is 0th ele making it circular

## Brute Force

Using 2 nested Loops 

For each element, we traverse all the other elements using % to access the 0th element after the last element (as N % N is 0)

If we found greater element then we use it, else we store -1

TC=O(N^2) and SC=O(N) for saving solution

## OPTIMAL approach using Monotonic Stack

We Imagine that we have Array as 2N

- Imagine array as 2N => [1,2,1] -> [1,2,1][1,2,1] , Same array is there after OG array
- We can access the current index using i%N
- Have array of N size, to store the ans (NGE), and have stack to get NGE
- Start iterating the Array from the last index of 2nd Array(repeated array's last index), index=2N-1
- We need to Move towards left, till we reach 0th index, very beginning of OG array
- Now for _i_ th index, pop the elements from stack which are lesser than or equals to nums[i]
- We don't store the solution (ans) till we reach our OG Array's last index, N-1 th index
- If we are on OG array (i<N), then we can store the ans as ans[i]= s.empty()? -1 : s.top()   // If empty stack, then -1, else stack's top
- We push the current element in the Stack s.push(nums[i%N]) 

```cpp
class Solution {
public:
    vector<int> nextGreaterElements(vector<int>& nums) {
        int n = nums.size();
        vector<int> ans(n); //To store NGE
        stack<int> st; // Used to get NGE
        for(int i = 2*n-1; i>=0; i--){  //Imagine array as 2N => [1,2,1] -> [1,2,1][1,2,1]
            //Can access current index using i%N
            while(!st.empty() && st.top()<=nums[i%n]){
                st.pop();
            }
            if(i < n){ //We don't store ans until we reach N-1, our original array's last index
                ans[i] = st.empty() ? -1 : st.top();
            }
            st.push(nums[i%n]);
        }
        return ans;
    }
};
```

TC=O(The loop runs 2N times + Total pushes = 2N + Total pops ≤ 2N) = O(6N) = O(N)

SC=O(2N for stack + N for ans) = O(N)

> A **monotonic stack** is a stack that maintains its elements in a specific order (either strictly increasing or strictly decreasing).

> Before pushing a new element, we pop elements that violate this order, allowing us to efficiently solve problems like **Next Greater Element**, **Next Smaller Element**, and **Stock Span** in `O(N)` time.
