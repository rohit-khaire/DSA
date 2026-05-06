# Merge Overlapping Subintervals

[LeetCode](https://leetcode.com/problems/merge-intervals/)

<br>

<img width="1009" height="480" alt="image" src="https://github.com/user-attachments/assets/cc4f07b4-4c37-46f8-902b-b4bb620c25ca" />


## Brute Force

1. **Sort** all subarrays by 1st ele in sub-array, if two sub-arrays are having equal 1st ele then sort them by 2nd ele

(2,4),(2,1),(2,5) => (2,1),(2,4),(2,5)

```
Ex. (1,3) , (2,6) , (8,9) , (9,11) , (8,10) , (2,4) , (15,18) , (16,17)

Sorted => (1,3) , (2,4) , (2,6) , (8,9) , (8,10) , (9,11) , (15,18) , (16,17)
```

2. Now keep two pointers on first sub-array (1,3)

Now check that next elements (sub-arrays) can be part of it or not (Current subA cha 1st ele < main Interval cha 2nd ele -> Change Interval)

Main Intervals : (1,3)

- (2,4) -> 2<3 so yes, Change interval to (1,4)

Main Intervals : (1,4)

- (2,6) -> 2<4 so yes, Change interval to (1,6)

Main Intervals : (1,6)

- (8,9) -> 8<6 No, so have new interval

Firstly move 2nd pointer ( which was on 1st subA ) and check that each subA is in the Main Interval or not by checking that 2nd ele of subA is < Main Interval 2nd ele, when it comes on (8,9) stop it there

Now stand on (8,9) with 2nd pointer, and look that who can be part of it using 1st pointer

Main Intervals : (1,6) , (8,9)

- (8,10) -> 8<9 so yes, Change the interval to (8,10)

Main Intervals : (1,6) , (8,10)

- (9,11) -> 9<10 so yes, Change the Interval to (8,11)

Main Intervals : (1,6) , (8,11)

- (15,18) -> 15<11 NO, so have interval but take same steps as previously taken

Move 2nd pointer which was standing on (8,9) and check that does each subA is in that interval or not

Main Intervals : (1,6) , (8,11) , (15,18)

Make 2nd pointer stand on (15,18) in Main Array, and check further subA using 1st pointer

- (16,17) -> 16<18 YES, Keep interval to (15,18)

**Main Intervals : (1,6) , (8,11) , (15,18)**


## Optimal Solution

**Just Don't have 2nd pointer** , Do everything with one pointer only

Visualize:

```
vector<vector<int>> arr:

| Start | End |
|-------|-----|
| 1     | 3   |
| 2     | 4   |
| 2     | 6   |
| 8     | 9   |
| 8     | 10  |
| 9     | 11  |
| 15    | 18  |
| 16    | 17  |
```

### CODE

```
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& arr) {
        int n= arr.size();
        vector<vector<int>> ans;
        sort(arr.begin(), arr.end());
        for(int i=0;i<n;i++){
            if(ans.empty() || arr[i][0] > ans.back()[1]){
                ans.push_back(arr[i]);
            }
            else if(arr[i][0] <= ans.back()[1]){   // Can also work fine with else
                ans.back()[1] = max(ans.back()[1], arr[i][1]);
            }
        }
        return ans;
    }
};
```

<br>


## 🔹 Step 1: Input

```
(1,3) , (2,6) , (8,9) , (9,11) , (8,10) , (2,4) , (15,18) , (16,17)
```

---

## 🔹 Step 2: After Sorting

C++ `sort()` sorts based on first element, then second:

```
(1,3), (2,4), (2,6), (8,9), (8,10), (9,11), (15,18), (16,17)
```

---

## 🔹 Step 3: Dry Run Loop

### 👉 i = 0 → (1,3)

* `ans` is empty → push

```
ans = [(1,3)]
```

---

### 👉 i = 1 → (2,4)

* Compare with last: (1,3)
* 2 ≤ 3 → overlap → merge
* max(3,4) = 4

```
ans = [(1,4)]
```

---

### 👉 i = 2 → (2,6)

* Compare with last: (1,4)
* 2 ≤ 4 → overlap → merge
* max(4,6) = 6

```
ans = [(1,6)]
```

---

### 👉 i = 3 → (8,9)

* Compare with last: (1,6)
* 8 > 6 → no overlap → push

```
ans = [(1,6), (8,9)]
```

---

### 👉 i = 4 → (8,10)

* Compare with last: (8,9)
* 8 ≤ 9 → overlap → merge
* max(9,10) = 10

```
ans = [(1,6), (8,10)]
```

---

### 👉 i = 5 → (9,11)

* Compare with last: (8,10)
* 9 ≤ 10 → overlap → merge
* max(10,11) = 11

```
ans = [(1,6), (8,11)]
```

---

### 👉 i = 6 → (15,18)

* Compare with last: (8,11)
* 15 > 11 → no overlap → push

```
ans = [(1,6), (8,11), (15,18)]
```

---

### 👉 i = 7 → (16,17)

* Compare with last: (15,18)
* 16 ≤ 18 → overlap → merge
* max(18,17) = 18

```
ans = [(1,6), (8,11), (15,18)]
```

---

## 🔹 Final Answer

```
[(1,6), (8,11), (15,18)]
```

---

## 🔥 Core Intuition

* **Sort intervals first**
* Always compare with **last merged interval**
* Two cases:

  * **No overlap** → push new interval in vector ans
  * **Overlap** → merge using `ans.back()[1] = max(ans.back()[1], arr[i][1])`
