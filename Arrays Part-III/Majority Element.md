# Majority Element

[LeetCode](https://leetcode.com/problems/majority-element/description/)

Problem Statement: Given an integer array nums of size n, return the majority element of the array.

The majority element of an array is an element that appears more than n/2 times in the array. The array is guaranteed to have a majority element.

## Brute Force

Start iterting through the array. And keep count for each element. 

Start with i to iterate each element

Start with j to match all elements in the array with a[i], it match then count++ and if count > n/2 ; That is majority element.

Simple:

* Iterate through the array to select each element one by one.

* For each selected element, run another loop to count its occurrences in the given array.

* If the occurrence of any element is greater than the floor of (N/2), return that element immediately as the majority element.

**SC = O(N^2)**

**TC = O(1)**

## Better (Use Map to keep {element,count} Beats 100%

> Map stores keys in ordered form

* Use a hashmap (map<int,int> mpp;) to store elements as (key, value) pairs, where the key is the element of the array and the value is the number of times it occurs.

> ``Why not hash array used? => As element can be anything, it's not limited by N, making hash array > N``

* Traverse the array and update the value of the corresponding key in the hashmap. {key,value} = {elemnt,count} so update count(value)

* Now check if the value (the count) of any key is greater than the floor of (N/2).

* If the value is greater than the floor of (N/2), return the key immediately as the majority element.

* If no majority element is found, continue iterating through the array.

* After iterating, if no element found with count > n/2, then return -1

Code:

```
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        map<int,int> mpp;
        int n = nums.size();
        for(int i=0;i< n;i++){
            mpp[nums[i]]++;
        }
        for(auto i: mpp){
            if(i.second > n/2){
                return i.first;
            }
        }
        return -1;
    }
};
```

**TC = O(N)** : This is because we are iterating through the array once to count occurrences and then iterating through the hashmap to find the majority element.

**SC = O(N)** : As we are using a hashmap to store the counts of each element, which can take up to N space in the worst case.


## Optimal - Using Moore's Voting Algorithm

The intuition behind this algo is that if an element appears more than n/2 times, then it remain after cancelling out all the other distinct elements.

It is majority as after removing distinct elements, majority stays

| Majority Elements | Distinct Minority Elements | After Pairwise Cancellation         |
| ----------------- | -------------------------- | ----------------------------------- |
| `+++++` (5)       | `---` (3)                  | `++` → Majority survives (`2` left) |

Explanation using Moore's Voting Algorithm:

* Each `-` cancels one `+`
* Since majority count is greater than `n/2`, some majority elements always remain
* Remaining count here: `5 - 3 = 2`


After applying Moore's Voting Algorithm, a second pass is required to verify if the candidate element (ele) actually appears more than n/2 times.

**A majority element survives even after cancelling out one occurrence of it with every occurrence of other elements.**

Algorithm:

* Initialize two variables: count (cnt) to track the count of elements, and element (ele) to keep track of the element being counted.

* Start Traversing through the given array. If count is 0, store the current value of the array as element (ele = nums[i]).

* If the current element in the array is the same as element, increment the count by 1.

* If the current element is different from element, decrement the count by 1.

* At the end of the traversal, the integer stored in ele variable will be the expected result (the majority element).

* Check/Verify this, by getting the count(cnt2) for that ele in the array. If it's count2 > n/2 ; return ele or else -1 for no majority

* At the end, cnt is useless and cnt2 can be used as count of majority element.

```
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        // A element that occurs more than n/2 - Moore's Voting Algo
        int cnt=0;
        int ele;
        int n = nums.size();
        for(int i=0;i<n;i++){
            if(cnt==0){
                ele = nums[i];
            }
            if(nums[i]==ele){
                cnt++;
            }else{
                cnt--;
            }
        }
        int cnt2=0;
        for(int i=0;i<n;i++){
            if(nums[i]==ele){
                cnt2++;
            }
        }
        if(cnt2 > n/2) return ele;
        return -1;
    }
};
```


**TC = O(N)**

**SC = O(1)**




