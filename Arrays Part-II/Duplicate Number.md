# Find the Duplicate Number

[LeetCode](https://leetcode.com/problems/find-the-duplicate-number/)

## Brute Force

1) Sort Array ( Modifies the Array )

2) Find a[i] where a[i]==a[i+1]

3) return that

TC = O(NlogN)

SC = O(1)

## Brute Force 2, Using Hashing

1) Create an extra array of size n (same size), fill all vals with 0

2) Start iterating main array, a[i] wali value will become index for us for new array

a[i]=2

b[2] = 1  // Convert 0 to 1, means done with 2

While upadting b, if it's already 1 there then that means it's the reapeated one.

So, return that number(It's duplicate value)

TC = O(N)

SC = O(N)

## Optimal Solution ( Linked List Cycle Method )

Start from index 0 and create a LinkedList for Visualization, print value at 0th index, then print value at arr[value], repeat printing again and again

<br>

<img width="597" height="127" alt="image" src="https://github.com/user-attachments/assets/8d4b5a11-f760-4031-9225-3f233a32dd64" />


```
For Array: {2,5,9,6,9,3,8,9,7,1}
```

# Algorithm (MOST IMPORTANT )
Initially, we have a linked list with values like: 2, 9, 1, 5, 3, 6, 8, 7, and then we reach back to 9, forming a cycle.

The slow and fast pointers both start at the first element of the list. The slow pointer moves one step at a time, and the fast pointer moves two steps at a time.

After a few steps, the slow and fast pointers will meet at an index (in this case, at 7).

Now, place the fast pointer back to the first element (2) and move both the slow and fast pointers one step at a time.

The point where the slow and fast pointers meet again will be the duplicate number in the list (in this case, 9).

Intuition: Since there is a duplicate number, a cycle is always formed. The first collision between slow and fast pointers guarantees that a cycle exists.

When slow and fast pointers meet, the distance between their collision points represents the cycle length. This allows us to find the duplicate number.

<br>
<img width="598" height="138" alt="ezgif-5c0c3607a58c7c07" src="https://github.com/user-attachments/assets/030ff810-933d-4405-9c3b-57f1dccce833" />



<br><br>

## CODE:

```
// find the duplicate using Floyd's Tortoise and Hare cycle detection
int findDuplicate(vector<int>& nums) {
  // initialize pointers at the start
  int slow = nums[0];
  int fast = nums[0];

  // move slow by 1 step and fast by 2 steps until they meet
  do {
    slow = nums[slow];
    fast = nums[nums[fast]];
  } while (slow != fast);

  // reset fast to start to find the entrance to the cycle
  fast = nums[0];

  // move both by 1 step until they meet at the duplicate
  while (slow != fast) {
    slow = nums[slow];
    fast = nums[fast];
  }

  // return the duplicate value
  return slow;
}
```

<br>

## Dry Run


Index mapping becomes:

| Index | Value |
| ----- | ----- |
| 0     | 2     |
| 1     | 5     |
| 2     | 9     |
| 3     | 6     |
| 4     | 9     |
| 5     | 3     |
| 6     | 8     |
| 7     | 9     |
| 8     | 7     |
| 9     | 1     |

The algorithm treats values as **next pointers**.

So traversal looks like:

```text
0 → 2 → 9 → 1 → 5 → 3 → 6 → 8 → 7 → 9 ...
```

Cycle starts at `9`, so duplicate = `9`.

---

# Phase 1: Detect Meeting Point ( Slow and Fast Pointer )

Initial:

```cpp
slow = nums[0] = 2
fast = nums[0] = 2
```

---

## Iteration 1

### slow moves 1 step

```cpp
slow = nums[2] = 9
```

### fast moves 2 steps

```cpp
fast = nums[ nums[2] ]
     = nums[9]
     = 1
```

| Pointer | Value |
| ------- | ----- |
| slow    | 9     |
| fast    | 1     |

---

## Iteration 2

### slow

```cpp
slow = nums[9] = 1
```

### fast

```cpp
fast = nums[ nums[1] ]
     = nums[5]
     = 3
```

| Pointer | Value |
| ------- | ----- |
| slow    | 1     |
| fast    | 3     |

---

## Iteration 3

### slow

```cpp
slow = nums[1] = 5
```

### fast

```cpp
fast = nums[ nums[3] ]
     = nums[6]
     = 8
```

| Pointer | Value |
| ------- | ----- |
| slow    | 5     |
| fast    | 8     |

---

## Iteration 4

### slow

```cpp
slow = nums[5] = 3
```

### fast

```cpp
fast = nums[ nums[8] ]
     = nums[7]
     = 9
```

| Pointer | Value |
| ------- | ----- |
| slow    | 3     |
| fast    | 9     |

---

## Iteration 5

### slow

```cpp
slow = nums[3] = 6
```

### fast

```cpp
fast = nums[ nums[9] ]
     = nums[1]
     = 5
```

| Pointer | Value |
| ------- | ----- |
| slow    | 6     |
| fast    | 5     |

---

## Iteration 6

### slow

```cpp
slow = nums[6] = 8
```

### fast

```cpp
fast = nums[ nums[5] ]
     = nums[3]
     = 6
```

| Pointer | Value |
| ------- | ----- |
| slow    | 8     |
| fast    | 6     |

---

## Iteration 7

### slow

```cpp
slow = nums[8] = 7
```

### fast

```cpp
fast = nums[ nums[6] ]
     = nums[8]
     = 7
```

| Pointer | Value |
| ------- | ----- |
| slow    | 7     |
| fast    | 7     |

Both meet → cycle detected.

---

# Phase 2: Find Entrance of Cycle

Reset:

```cpp
fast = nums[0] = 2
slow = 7
```

---

## Iteration 1

### slow

```cpp
slow = nums[7] = 9
```

### fast

```cpp
fast = nums[2] = 9
```

| Pointer | Value |
| ------- | ----- |
| slow    | 9     |
| fast    | 9     |

They meet at `9`.

# Final Answer

```cpp
Duplicate element = 9
```

---

# Visual Understanding

```text
0 → 2 → 9 → 1 → 5 → 3 → 6 → 8 → 7
          ↑                   ↓
          ← ← ← ← ← ← ← ← ← ←
```

Cycle entrance = duplicate number = `9`.

---

# Time & Space Complexity

## Time Complexity

```text
O(N)
```

* Floyd detection: O(N)
* Finding cycle entrance: O(N)

---

## Space Complexity

```text
O(1)
```

Only two pointers are used.




