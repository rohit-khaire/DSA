# Majority Element II

[LeetCode](https://leetcode.com/problems/majority-element-ii/)

Majority Elements( < N/3 times) | Find the elements that appears more than N/3 times in the array

Problem Statement: Given an integer array nums of size n. Return all elements which appear more than n/3 times in the array. The output can be returned in any order.

**There cannot be more than 2 majority elements** <br>
To understand why there can't be more than two majority elements (elements that appear more than n/3 times) in an array of size n, let's consider the following reasoning: <br>
A majority element must appear more than n/3 times. Let’s assume there are more than two majority elements, say A, B, and C. <br>
The combined frequency of these three elements would be: frequency of A + frequency of B + frequency of C > n/3 + n/3 + n/3 = n. <br>
Since the total occurrences of all elements cannot exceed n (the size of the array), the combined frequency of any three elements each appearing more than n/3 times would exceed the total size of the array, leading to a contradiction. <br>
Therefore, it is mathematically impossible to have more than two elements that each appear more than n/3 times in the array. <br>


As whole array = 1

<h3>1/3 + 1/3 + 1/3 = 1 => Three Parts are there</h3>

|   |   |   |
| - | - | - |


We want elements appearing more than 1/3 times, means exceeding 1 box, so there can be max 2 eles which can exceed a single box each


## Brute Force

* Iterate through the array and select each element one by one.
* For each unique element, run another loop to count its occurrences in the array.
* If any element occurs more than floor(N/3) times, include it in the result array.
* If a previously included element is found during traversal, skip it to avoid counting duplicates.
* If the result array already contains 2 elements, break out of the loop, as there can’t be more than two majority elements.
* Return the result array containing the majority elements or return -1 if no such element is found.

**TC = O(n^2) and SC = O(1)**

## Better Solution using HashMap

Like previously doing with Majority Element.md using HashMap

```cpp
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
        map<int,int> mpp;
        int n = nums.size();
        vector<int> result;
        for(int i=0;i<n;i++){
            mpp[nums[i]]++;
            if(mpp[nums[i]] == int(n/3)+1) result.push_back(nums[i]);
            if(result.size() == 2) break;
        }
        return result;
    }
};
```


**TC = O(n) and SC = O(n)**

## Optimal Solution

