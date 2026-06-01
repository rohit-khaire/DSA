# Longest Consecutive Sequence in an Array

[NeetCode](https://neetcode.io/problems/longest-consecutive-sequence/)

[LeetCode](https://leetcode.com/problems/longest-consecutive-sequence/)

Solved on Both

Problem Statement: Given an array nums of n integers.

Return the length of the longest sequence of consecutive integers. The integers in this sequence can appear in any order.

Example: 

Input: nums = [100,4,200,1,3,2] <br>
Output: 4 <br>
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4. <br>
(n,n+1,(n+1)+1,....)

# BRUTE Force

- As you iterate through each number in the array, begin by checking if consecutive numbers like (x+1, x+2, x+3), and so on, exist in the array. The occurrence of the next consecutive number can be checked by using a linear search.
- When you find consecutive numbers, start counting them using a counter. Increment this counter each time you find the next consecutive number in the sequence.
- This counter effectively keeps track of how long the current consecutive sequence is as you move through the array and find more consecutive numbers.

```cpp
public:
    // Function to find the longest consecutive sequence
    int longestConsecutive(vector<int>& nums) {
        // If the array is empty
        if (nums.size() == 0) {
            return 0;
        }
        int n = nums.size();
        // Initialize the longest sequence length
        int longest = 1; 

        // Iterate through each element in the array
        for (int i = 0; i < n; i++) {
            // Current element
            int x = nums[i]; 
            // Count of the current sequence
            int cnt = 1; 

            // Search for consecutive numbers
            while (linearSearch(nums, x + 1) == true) {  // linear search for x+1 in nums
                // Move to the next number in the sequence
                x += 1; 
                // Increment the count of the sequence
                cnt += 1; 
            }

            // Update the longest sequence length found so far
            longest = max(longest, cnt);
        }
        return longest;
    }
};
```

**TC=N*N  and SC=O(1)**

where N is the number of elements in the array. This is because for each element, we may need to perform a linear search through the entire array to find consecutive numbers.


## BETTER by Sorting the Array and using O(N) TC

We sort the array and then iterates the array only once from 0 to n-1

We keep track of using variables, 

*cnt* is used to count the current length, it's reset to 1 when any new element appears other than expected, resets when one sequence is ended or breaked

Resets to 1 as the only one element can only be a sequence with length as 1

*last* used to store the last element, which is used to check with the current element, if last == nums[i] , then we can increment the *cnt* 

and to move further we can set current element as last. Last stands for last element of the sequence, and hence when the sequence ends, we can say that I (current element) is the first and last element of new sequence

*largestLength* is the variable used to return the maximum count obtained till now, which represents the longest consicutive sequence

A short **revision algorithm** for your approach:

### Algorithm (Sorting Approach)

1. Sort the array.
2. Initialize:

   * `last = INT_MIN`
   * `cnt = 0`
   * `largestLength = 0`
3. Traverse each element:

   * If current element is a duplicate (`nums[i] == last`), skip it.
   * If current element is **not consecutive** (`nums[i] - 1 != last`):

     * Start a new sequence → `cnt = 1`
   * Else (current element is consecutive):

     * Extend sequence → `cnt++`
   * Update `last = nums[i]`
   * Update answer: `largestLength = max(largestLength, cnt)`
4. Return `largestLength`.

### Memory Trick

**"Sort → Skip Duplicates → Check Consecutive → Count Length → Update Maximum"**

Example:
`[100,4,200,1,3,2]`

After sorting:
`[1,2,3,4,100,200]`

```
1 → cnt=1
2 → cnt=2
3 → cnt=3
4 → cnt=4
100 → reset cnt=1
200 → reset cnt=1
```

Answer = **4**

```cpp
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        int n = nums.size();
        int cnt,last=INT_MIN,largestLength=0;
        for(int i=0;i<n;i++){ // 2,3,4,4,5,10,20
            if(nums[i]==last) continue;
            if(nums[i]-1 != last){
                cnt=1;
                last=nums[i];
            }else if(nums[i]-1 == last){
                cnt++;
                last=nums[i];
            }
            largestLength=max(largestLength,cnt);
        }
        return largestLength;
    }
};
```

**TC:** `O(nlogn)+O(n)` (sorting and iteration)

**SC:** `O(1)` 

## OPTIMAL APPROACH


Use unorder_set to remove all the duplicates, now start iterating the set itself, if the current element is not the starting element in sequence ( there exists x-1 element in the set), then just skip as We will only be working when the current is the First element of sequence. If current element is the first element of sequence then we just copy it and increase the count until there is no further sequnece availabe ( not x+1 exists in set). And then select max from cnt and longestLength.

```cpp
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        unordered_set<int> st;
        for(int i=0;i<nums.size();i++){
            st.insert(nums[i]);
        }
        int cnt,longestLength=0;
        for(auto curr: st){
            if(st.count(curr-1)) continue; //current-1 exists
            else{
                // I am the starting
                cnt=1;
                int temp=curr;
                while(st.count(temp+1)){
                    cnt++;
                    temp+=1;
                }
                longestLength=max(longestLength,cnt);
            }
        }
        return longestLength;
    }
};
```

### Why it works

* The set removes duplicates.
* A number is a **starting point** only if `curr - 1` is not present.
* From each starting point, you keep extending the sequence.
* Every number is effectively processed at most once across all `while` loops.

### Complexity

* Insert into set: **O(n)** average
* Traverse set: **O(n)** average
* Sequence expansion: **O(n)** total average

**TC:** `O(n)` average
**SC:** `O(n)`

### Small Revision Note

**Algorithm:**

1. Insert all elements into a hash set.
2. For each number:

   * If `num - 1` exists → skip.
   * Otherwise, start a sequence.
3. Count consecutive numbers using `while(num + 1 exists)`.
4. Update maximum length.
5. Return maximum length.


