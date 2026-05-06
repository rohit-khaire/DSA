# Insert Interval

[LeetCode](https://leetcode.com/problems/insert-interval/)

Given sorted intervals, add a given interval in sorted Intervals and handle if overlapping

```
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& arr, vector<int>& newInterval) {
        vector<vector<int>> ans;
        int i = 0, n = arr.size();

        // 1. Add all intervals before newInterval
        while (i < n && arr[i][1] < newInterval[0]) {
            ans.push_back(arr[i]);
            i++;
        }

        // 2. Merge overlapping intervals
        while (i < n && arr[i][0] <= newInterval[1]) {
            newInterval[0] = min(newInterval[0], arr[i][0]);
            newInterval[1] = max(newInterval[1], arr[i][1]);
            i++;
        }

        // Add merged interval
        ans.push_back(newInterval);

        // 3. Add remaining intervals
        while (i < n) {
            ans.push_back(arr[i]);
            i++;
        }

        return ans;
    }
};
```
<br>
This solution beats 100%

Let’s do a **clean dry run** with a typical example so you can *see the flow clearly*.

---

## ✅ Example Input

```
arr = [[1,3], [6,9]]
newInterval = [2,5]
```

---

## 🔁 Step-by-step Dry Run

### Initial State:

```
ans = []
i = 0
n = 2
```

---

## 🔹 Step 1: Add intervals before newInterval

Condition:

```
arr[i][1] < newInterval[0]
```

👉 Check:

```
arr[0] = [1,3]
3 < 2 ❌ (false)
```

➡️ No intervals added

---

## 🔹 Step 2: Merge overlapping intervals

Condition:

```
arr[i][0] <= newInterval[1]
```

---

### 👉 Iteration 1:

```
arr[0] = [1,3]
1 <= 5 ✅
```

Merge:

```
newInterval[0] = min(2,1) = 1
newInterval[1] = max(5,3) = 5
```

Now:

```
newInterval = [1,5]
i = 1
```

---

### 👉 Iteration 2:

```
arr[1] = [6,9]
6 <= 5 ❌
```

➡️ Stop merging

---

### Add merged interval:

```
ans = [[1,5]]
```

---

## 🔹 Step 3: Add remaining intervals

```
i = 1
```

Add:

```
ans = [[1,5], [6,9]]
```

---

## ✅ Final Output:

```
[[1,5], [6,9]]
```

---

# 🔥 Key Intuition (Important for interviews)

### 3 zones:

1. **Before overlap** → directly push
2. **Overlap zone** → merge into `newInterval`
3. **After overlap** → directly push

---

# ⚡ Quick Edge Case (Very Important)

### Case:

```
arr = []
newInterval = [4,8]
```

👉 Step 1 & 2 skip (n = 0)

➡️ Directly:

```
ans = [[4,8]]
```

---

# 💡 Why this approach is clean

* Single pass → **O(n)**
* No extra sorting needed
* No unnecessary comparisons



