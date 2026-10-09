[Leetcode](https://leetcode.com/problems/spiral-matrix/description/)

<img width="322" height="242" alt="image" src="https://github.com/user-attachments/assets/b7733f8f-744e-4d45-b729-0665a4950f33" />

Output: An array => [1,2,3,4,8,12,11,10,9,5,6,7]

# Approach - Keep 4 boundaries and shrink them

<img width="322" height="242" alt="image" src="https://github.com/user-attachments/assets/29621bf9-216a-4042-9275-b4b9d96f82a0" />


## Spiral Matrix — Algorithm (Revision Notes)

1. Initialize four boundaries: `left = 0`, `right = cols - 1`, `top = 0`, `down = rows - 1`.

2. While `left <= right && top <= down`:

   * Left → Right: Traverse the top row, then `top++`.

   * Top → Bottom: Traverse the right column, then `right--`.

   * Right → Left: IF `top <= down`, traverse the bottom row, then `down--`.

   * Bottom → Top: IF `left <= right`, traverse the left column, then `left++`.

3. Return the answer array.

### ⚠️ Remember the two `if` conditions!

* `if (top <= down)` → before traversing the bottom row.

* `if (left <= right)` → before traversing the left column.

Why? After the first two traversals, the remaining boundaries might cross. These checks prevent duplicate elements when only one row or one column remains.

Quick memory trick: → ↓ ← ↑, then shrink boundaries inward. The last two directions need `if` checks!


```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int left=0; // V
        int right = matrix[0].size()-1; //         V
        int top = 0; // >
        int down = matrix.size()-1; // >
        vector<int> ans;
        while(left<=right && top<=down){
            for(int i=left;i<=right;i++){
                ans.push_back(matrix[top][i]);
            }
            top++;
            for(int i=top;i<=down;i++){
                ans.push_back(matrix[i][right]);
            }
            right--;
            if(top<=down){
                for(int i=right;i>=left;i--){
                    ans.push_back(matrix[down][i]);
                }
                down--;
            }
            if(left<=right){
                for(int i=down;i>=top;i--){
                    ans.push_back(matrix[i][left]);
                }
                left++;
            }
        }
        return ans;
    }
};
```

TC:O(MxN) and SC:O(1)
