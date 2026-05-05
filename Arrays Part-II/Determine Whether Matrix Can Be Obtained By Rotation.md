# Determine Whether Matrix Can Be Obtained By Rotation

[LeetCode](https://leetcode.com/problems/determine-whether-matrix-can-be-obtained-by-rotation/description/)

<br>
<img width="589" height="290" alt="image" src="https://github.com/user-attachments/assets/b3cda6c3-5730-439e-8187-7a93b7b68f47" />
<br>

### Determine whether *target* matrix can be obtained by rotating matrix *mat*

Rotating matrix mat and checking each time that does it matches target matrix

## 🔁 Core Idea (1 line)

To rotate a matrix **90° clockwise** → **Transpose + Reverse each row**

---

## 🧠 Step-by-Step Logic

### 1. 🔄 Transpose the matrix

Convert rows → columns

👉 Swap elements across diagonal:

```
mat[i][j] ↔ mat[j][i]   (only for j > i)
```

✔ Why `j = i+1`?
To avoid swapping twice and skipping diagonal elements.

---

### 2. 🔁 Reverse each row

After transpose, reverse every row to complete **90° clockwise rotation**

```
[1 2 3]      [1 4 7]      [7 4 1]
[4 5 6]  →   [2 5 8]  →   [8 5 2]
[7 8 9]      [3 6 9]      [9 6 3]
```

---

## 🔁 Full Rotation Logic

```
1 Rotation = Transpose + Reverse Rows
```

---

## 🔍 `findRotation` Logic

Try all 4 possible rotations:

```
0°   → original
90°  → 1 rotation
180° → 2 rotations
270° → 3 rotations
```

### Loop:

* Check if `mat == target`
* If yes → return true
* Else → rotate matrix
* Try max 4 times

---

## ⚡ Final Intuition (Super Short)

👉 “Rotate matrix = Flip across diagonal + Reverse rows”
👉 “Try 4 rotations → if any matches target → true”

---

## 🧠 Memory Trick

Think:

> **"Diagonal flip, then row flip = rotation done"**

---

## 🚫 Common Mistake (Important)

If you don’t pass matrix by reference:

```
vector<vector<int>> mat
```

instead of:

```
vector<vector<int>> &mat
```

👉 Rotation won’t affect original matrix → always false ❌


CODE ( Beats 100% ):

```
class Solution {
public:
    void rotateMat(vector<vector<int>> &mat){
        int n= mat.size();
        for(int i=0;i<n-1;i++){
            for(int j=i+1;j<n;j++){
                swap(mat[i][j],mat[j][i]);
            }
        }
        for(int i=0;i<n;i++){
            reverse(mat[i].begin(),mat[i].end());
        }
    }
    bool findRotation(vector<vector<int>>& mat, vector<vector<int>>& target) {
        for(int i = 0; i < 4; i++){
            if(mat == target) return true;
            rotateMat(mat);
        }
        return false;
    }
};
```
