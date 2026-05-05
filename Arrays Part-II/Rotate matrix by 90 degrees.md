# Rotate matrix by 90 degrees / Rotate Image

[LeetCode](https://leetcode.com/problems/rotate-image/)

<img width="522" height="260" alt="image" src="https://github.com/user-attachments/assets/3728f461-b851-4a70-82af-cbdf66ea625b" />

Type of Rows converted to Columns

## Brute Force

Creating a new Array, and picking up eles from Main Array and putting the eles on their expected positions in newArray

<img width="963" height="632" alt="image" src="https://github.com/user-attachments/assets/7a21f0be-1d20-40f4-969b-188b18438605" />


We notice a pattern in it:

n=4 

**[i][j] -> [j][ (n-1)-i ]**

```
ans[n][n]
for(i=0 ->n-1){
  for(j=0->n-1){
      ans[j][n-1-i] = arr[i][j];
  }
}
return ans;
}

```

TC -> O(n^2)

SC -> O(n^2)


## Optimal Solution

**Transpose -> Reverse the Rows**

1. Transpose

Diagonal Elements stays there only

<img width="431" height="669" alt="image" src="https://github.com/user-attachments/assets/24e67ff4-92ba-4d44-80d9-c40c5d2645bb" />


Notice that only non-diagonal are changing their positions, that to they are swapped like [i][j] by [j][i]


<img width="354" height="394" alt="image" src="https://github.com/user-attachments/assets/bc309285-fc6d-4932-b15c-ddda3a9a2e0a" />

You need to traverse only the right upper triangle, and just start swapping

To traverse the upper triangle, notice the pattern, as you can see in above image:

for 0 -> j is 1,2,3

for 1 -> j is 2,3

for 2 -> j is 3

So, i -> from i+1 to n-1

2. Reverse the rows

Now reverse the rows to get final matrix

<img width="248" height="181" alt="image" src="https://github.com/user-attachments/assets/9989be87-7908-4b5d-a2fa-b0c4b7dc85ea" />

<br>

```
## Rotate Matrix by 90° (Clockwise)

### Original Matrix (4x4)

| 1  | 2  | 3  | 4  |
| 5  | 6  | 7  | 8  |
| 9  | 10 | 11 | 12 |
| 13 | 14 | 15 | 16 |

---

### Step 1: Transpose Matrix (swap rows ↔ columns) ( Code : Keeping diag elemts as it is and just swap non-diag eles)

| 1  | 5  | 9  | 13 |
| 2  | 6  | 10 | 14 |
| 3  | 7  | 11 | 15 |
| 4  | 8  | 12 | 16 |

---

### Step 2: Reverse Each Row

| 13 | 9  | 5  | 1  |
| 14 | 10 | 6  | 2  |
| 15 | 11 | 7  | 3  |
| 16 | 12 | 8  | 4  |

### Final Rotated Matrix (90° Clockwise)
```

## CODE:

```
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size();
        for (int i=0;i<=(n-1-1);i++){     # Transpose O(n/2 * n/2)
            for(int j=i+1;j<=n-1;j++){
                swap(matrix[i][j],matrix[j][i]);
            }
        }
        for(int i=0;i<n;i++){             # Reverse the Rows O(n/2), considering that using 2 pointers (start and end) swapping the start and end
            reverse(matrix[i].begin(), matrix[i].end());
        }
    }
};
```
<br>

TC => 

## Step 1 : Transpose

* Outer loop runs ≈ **n times**
* Inner loop runs:

  * For i = 0 → n-1 times
  * For i = 1 → n-2 times
  * For i = 2 → n-3 times
  * ...

 Total operations:
[
(n-1) + (n-2) + (n-3) + ... + 1
]

This is:
n(n-1)/2 is approx O(n^2)

###  Conclusion:

**Transpose = O(n²)**


## Step 2: Reverse Each Row

* There are **n rows**
* Each `reverse()` takes **O(n)**

 Total:
[
n \times n = O(n^2)
]

###  Conclusion:

**Reverse rows = O(n²)**

---

##  Final Time Complexity

[
O(n^2) + O(n^2) = 2(n^2) = O(n^2)
]

### Final Answer:

* Time Complexity = **O(n²)**

* Space Complexity = **O(1)**
