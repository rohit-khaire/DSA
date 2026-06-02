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






