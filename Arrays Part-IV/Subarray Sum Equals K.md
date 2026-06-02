# Subarray Sum Equals K

[LeetCode](https://leetcode.com/problems/subarray-sum-equals-k/description/)

Given an array of integers nums and an integer k, return the total number of subarrays whose sum equals to k.

*A subarray is a contiguous non-empty sequence of elements within an array.*

Subarray is contiguous part of array, 

{1,2,3,4}

{1,4} is *NOT* a subarray, but {1},{1,2},{1,2,3},{2,3},etc. ARE subarray

## Better Solution using HashMap to store sum and index

> **This solution is OPTIMAL solution when there are Positives,0s, and Negatives in the Array**

<img width="344" height="293" alt="image" src="https://github.com/user-attachments/assets/9799dcd4-5973-4d40-8a6c-845f5f3bb927" />


Logic: 

X = (X-K) + K = remaining + K

(X-K) = remaining

IF remianing exists in the map, then our subArray is from mpp[rem]+1(Index at which the sum is equals to remaining+1) to currentIndex(i)



### Easy-to-Remember Logic

Think:

> **"If current sum is `sum`, then I need an earlier prefix sum of `sum - k`."** (Part left of K)

Because:

```
currentSum - previousPrefixSum = k
```

So,

```
previousPrefixSum = currentSum - k
```

---

## Algorithm (Interview-Friendly)

### Step 1: Create a map

Store:

``
prefixSum
``

Store {SUM,index} to show that, AT THIS INDEX SUM IS THIS

---

### Step 2: Traverse the array

For each element:

```
sum += arr[i]
```

---

### Step 3: Check if sum itself is k

If:

```
sum == k
```

then subarray is from:

```
0 to i
```

Length:

```
i + 1
```

Update answer. MAX Length.

---

### Step 4: Check for (sum - k) (which is left part of K, SUM=left_part+k)

Compute Remaining:

```
rem = sum - k
```

If `rem` exists in map: At what index sum was == remaining

```
sum - rem = k
```
which means, sum=remaining+k

So subarray exists from:

```
map[rem] + 1
to
i
```

Length:

```
i - map[rem]
```

Update answer.

---

### Step 5: Store prefix sum(At what index, sum was what) only once

```cpp
if(prefixSum not present)
    store it
```

Why?

For longest length, we need the **earliest occurrence** of that prefix sum.

---

Remember:

> **Current Sum − Old Sum = K**

So find the **old sum**:

```cpp
oldSum = currentSum - k
```

If that old sum existed before, the part in between sums to `k`.

---

## Visual Example

Array:

```
[1, 2, 3, 1, 1, 1]
k = 6
```

| i | arr[i] | Prefix Sum | sum-k | Found?               |
| - | ------ | ---------- | ----- | -------------------- |
| 0 | 1      | 1          | -5    | No                   |
| 1 | 2      | 3          | -3    | No                   |
| 2 | 3      | 6          | 0     | sum==k → len=3       |
| 3 | 1      | 7          | 1     | Yes at idx 0 → len=3 |
| 4 | 1      | 8          | 2     | No                   |
| 5 | 1      | 9          | 3     | Yes at idx 1 → len=4 |

Answer = **4**

Subarray:

```
[3,1,1,1]
```

---


```
Time Complexity (TC) <br>
We traverse the array once → O(N)
Each map operation (find, insertion) in std::map takes O(log N)

So: TC=O(NlogN)

SC=O(N)

```


## OPTIMAL SOLUTION Only works when there are only Positives in the Array

We use **2 Pointers + Greedy** Approach

Very Very Simple Solution

There will 2 pointers i(left) and j(right)

**How the 2-Pointer approach works for positives/zeros:**
1.  **Expand:** Move a `right (j)` pointer to add elements to your current sum.
2.  **Shrink:** If the current sum exceeds $K$, move a `left(i)` pointer to remove elements from the start until the sum is less than or equal to $K$.
3.  **Update:** Whenever the sum exactly equals $K$, compare the current length ($right - left + 1$) with the maximum length found so far.

Because each pointer only traverses the array at most once, the total time complexity is linear, making it the most efficient solution for non-negative arrays.

**For Longest Subarray Length:**

For **non-negative numbers (positive + zeros)**, this version is correct.

### Let's test some edge cases

#### Case 1: Normal positive numbers

```cpp
nums = [1,2,3,2,5]
k = 5
```

Finds:

* [2,3] → length 2
* [5] → length 1

Returns 2 ✅

---

#### Case 2: Zeros included

```cpp
nums = [0,0,0,5]
k = 5
```

Finds:

* [0,0,0,5] → length 4

Returns 4 ✅

---

#### Case 3: k = 0

```cpp
nums = [0,0,0]
k = 0
```

Your code keeps extending:

* length 1
* length 2
* length 3

Returns 3 ✅

---

#### Case 4: No valid subarray

```cpp
nums = [1,2,3]
k = 10
```

Returns 0 ✅

---

### One small simplification

The same logic can be written more cleanly:

```cpp
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        long long sum = 0;
        int longestLength = 0;
        int i = 0;

        for(int j = 0; j < nums.size(); j++) {
            sum += nums[j];

            while(sum > k && i <= j) {
                sum -= nums[i];
                i++;
            }

            if(sum == k) {
                longestLength = max(longestLength, j - i + 1);
            }
        }

        return longestLength;
    }
};
```

### Important limitation

This is **not correct if negative numbers exist**.

Example:

```cpp
nums = [2, -1, 2]
k = 3
```

Longest subarray is the whole array (length 3), but sliding window logic breaks because removing elements does not necessarily decrease the sum when negatives are present.

### Complexity

* Time: **O(n)** (each element enters and leaves the window at most once)
* Space: **O(1)**

```cpp
MY VERSION
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        long long sum=0;
        int longestLength =0;
        int i=0,j=0;
        while(j<nums.size() && i<=j){
            sum+=(long long)nums[j];
            if(sum==k){
                int length = j-i+1;
                longestLength=max(longestLength,length);
            }
            else if(sum>k){
                while(sum>k && i<=j){
                    sum-=(long long)nums[i];
                    i++;
                }
                if(sum==k){
                    int length = j-i+1;
                    longestLength=max(longestLength,length);
                }
            }
            j++;
        }
        return longestLength;
        
    }
};
```


**For Count of subarrays with sum equals to K:**

Using HashMap to store sum and it's frequency

Similar logic applied as of BETTER solution above

```cpp
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        unordered_map<int,int> mpp;
        int cnt=0;
        long long sum=0;
        mpp[0]=1;  // For 0th index
        for(int i=0;i<nums.size();i++){
            sum+=nums[i];
            if(mpp.find(sum-k)!=mpp.end()){
                cnt+=mpp[sum-k];
            }
            mpp[sum]++; //Increment the frequency by 1 where key==sum
            

        }
        return cnt;
    }
};
```


Let's build the intuition from scratch.

### What does a prefix sum mean?

Suppose:

```cpp
nums = [1, 1, 1]
k = 2
```

Prefix sums:

```text
Index:      0   1   2
nums:       1   1   1
prefixSum:  1   2   3
```

At index 2:

```cpp
prefixSum = 3
```

We want a subarray with sum = 2.

So we ask:

```cpp
3 - ? = 2
```

which means:

```cpp
? = 1
```

Have we seen prefix sum `1` before?

Yes, once.

Therefore there is **1 subarray** ending at index 2 whose sum is 2.

---

## Why frequency and not just existence?

Consider:

```cpp
nums = [0,0,0]
k = 0
```

Prefix sums:

```text
0, 0, 0
```

Let's track frequencies.

Initially:

```cpp
freq[0] = 1
```

(the empty prefix)

---

### Index 0

```cpp
prefixSum = 0
```

Need:

```cpp
prefixSum - k = 0
```

How many times have we seen 0 before?

```cpp
freq[0] = 1
```

So:

```cpp
count += 1
```

Subarray found:

```text
[0]
```

Now:

```cpp
freq[0] = 2
```

---

### Index 1

```cpp
prefixSum = 0
```

Need:

```cpp
0 - 0 = 0
```

How many previous 0's?

```cpp
freq[0] = 2
```

So:

```cpp
count += 2
```

Why 2?

Because there are **2 different starting points**:

```text
[0]      (index 1)
[0,0]    (index 0..1)
```

Now:

```cpp
freq[0] = 3
```

---

### Index 2

Again:

```cpp
prefixSum = 0
freq[0] = 3
```

So:

```cpp
count += 3
```

Subarrays:

```text
[0]
[0,0]
[0,0,0]
```

---

Total:

```cpp
1 + 2 + 3 = 6
```

which is correct.

---

## The key insight

When you are at some index:

```cpp
count += freq[prefixSum - k];
```

means:

> "The value `prefixSum-k` has appeared `freq[prefixSum-k]` times before, and **each occurrence creates a different valid subarray ending here**."

That's why we store **frequency**, not just whether it exists.

### Memory trick

```text
For every current prefix sum:

How many previous prefix sums equal (prefixSum - k)?

Answer = frequency of (prefixSum - k).
```

So:

```cpp
count += freq[prefixSum - k];
freq[prefixSum]++;
```

This single pair of lines is the entire logic of LeetCode 560. 
