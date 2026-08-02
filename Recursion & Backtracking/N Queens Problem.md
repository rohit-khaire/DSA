# N Queen Problem

[Leetcode](https://leetcode.com/problems/n-queens/)

Place N queens in NxN chessboard(2D matrix) such that

- Each column has only 1 Queen
- Each row has only 1 Queen
- No Queen can attack each other

A queen can move in All Directions:

<img width="501" height="350" alt="image" src="https://github.com/user-attachments/assets/3a2e417d-37b7-46ef-9bec-6c465d68035d" />


But as we solve from left to right columnwise, while placing Queen on current location, we just need to check for any attacking Queen on left directions only

# Approach - Recursive

Using Recursion, we try all possible moves, and get the result/answer.

We try placing queen on each location and check whether it can be placed or not.


# Algorithm - Simple, Searches for Other Queen in all directions



<img width="1366" height="767" alt="image" src="https://github.com/user-attachments/assets/dfc4dabb-fa9d-43dc-8b9a-f8aabac971c4" />



- ``solveNQueens`` is the main function which gets called from main
  - We create one vector<vector<string>> ans; This stores our final answer, Which are chessboards with arrangements of Queen
  - We create one vector<vector<char>> temp(n, vector<char>(n, '.')); This is our temporary chessboard, this will be used to check all possible moves. - means empty position and Q means Q is placed. As we need to allow to change each element [i][j] , we are having characters, so that - can be replaced by Q and vice versa.
  -  Call solve(0,temp,ans,n); function, 0 means work on 0th column, temp is temp chessboard, ans is final chessboards, n means matrix is of NxN
 
<br>

- ``void solve(int col, vector<vector<char>> &board, vector<vector<string>> &ans, int n)`` function, used to try all possible moves in a given Column, this is recursive function, will be called with different columns
  - Forget about base case
  - Now for current given column, try all possible moves, try placing Queen at each row of current Column one by one
  - Start a loop(row=0 to N-1) //Try placing Queen at each row of given column
    - check if can I place Queen at current row of given column using Function Call
      - Yes, then place Queen at current row & call ``solve(col + 1, board, ans, n);`` passing col+1 so that If I place Queen at current row in given column, check for next column, that in next column, can I place Queen, check using solve function
      - Get back to normal form by   board[row][col] = '.';     so that for next row can Queen can be placed
  - **Base Case:** if current row is N, means we are successfully at the ends and can store chessboard as answer
    - Convert each row of characters to string, push string in vector of strings
    - Push this vector in answer
   

<br>

- ``canPlace()`` function used to check whether the Queen can be placed in current [row][col] or not, by checking is there any Queen in left directions or not?
  - If there is attacking Queen in current row, or left-Up direction, or left-Down direction, then return False, as cannot place Queen at this index
  - else return True
 

<img width="227" height="201" alt="image" src="https://github.com/user-attachments/assets/c05f67fe-9b36-4bd4-80e5-6dd53e4dfc92" />

 
**In Optimized Version: We use hash instead of searching for Queen each time in all left directions**



```cpp
class Solution {
public:
    bool canPlace(int row, int col, vector<vector<char>> &board, int n) {
        // Check all columns to the left in the same row
        for (int j = 0; j < col; j++) {
            if (board[row][j] == 'Q') return false;
        }

        // Check upper-left diagonal
        for (int i = row, j = col; i >= 0 && j >= 0; i--, j--) {
            if (board[i][j] == 'Q') return false;
        }

        // Check lower-left diagonal
        for (int i = row, j = col; i < n && j >= 0; i++, j--) {
            if (board[i][j] == 'Q') return false;
        }

        // Return true if no attack is possible
        return true;
    }

    // Backtracking function to place queens column by column
    void solve(int col, vector<vector<char>> &board,
               vector<vector<string>> &ans, int n) {
        // If all columns are filled, add current board to answer
        if (col == n) {
            vector<string> temp;
            for (int i = 0; i < n; i++) {
                // Convert row vector to string
                string row(board[i].begin(), board[i].end());
                temp.push_back(row);
            }
            ans.push_back(temp);
            return;
        }

        // Try placing queen in all rows of current column
        for (int row = 0; row < n; row++) {
            // Place queen only if safe
            if (canPlace(row, col, board, n)) {
                // Place queen
                board[row][col] = 'Q';
                // Recurse for next column
                solve(col + 1, board, ans, n); 
                // Backtrack and remove queen
                board[row][col] = '.';        
            }
        }
    }
    vector<vector<string>> solveNQueens(int n) {
        vector<vector<string>> ans;
        // vector<vector<string>> temp(n,0);
        vector<vector<char>> temp(n, vector<char>(n, '.'));
        solve(0,temp,ans,n);
        return ans;
    }
};
```


# Optimzed - Replace searching with Hashing

We keep 3 Extra Spaces for Hashing

Instead of checking every row, column, and diagonal every time we place a queen (which is slow), we use precomputed boolean arrays to instantly check if a queen can be safely placed. Each array acts like a hash for fast lookup. A row array keeps track of which rows already have a queen. Two diagonal arrays (lowerDiagonal and upperDiagonal) keep track of the diagonals that are under attack. This avoids repetitive scanning and makes the backtracking highly efficient.
- Initialize three boolean arrays, one for rows, one for lower diagonals, and one for upper diagonals.
- Start placing queens column by column from left to right using backtracking.
- For a given column, iterate through all rows and check if placing a queen at (row, col) is safe using the hash arrays.
- To check if placing a queen is safe, ensure the corresponding row, lower diagonal (row + col), and upper diagonal (n - 1 + col - row) are not already marked as attacked in the boolean arrays.
- If safe, place the queen and mark the corresponding row and diagonals as attacked.
- Recurse to the next column to place the next queen.
- When backtracking, remove the queen and unmark the row and diagonals to try other configurations.
- Count or store the solution if all columns are successfully filled with safe placements.



<img width="2105" height="1562" alt="image" src="https://github.com/user-attachments/assets/a42ca77c-3df9-4f03-b539-f944cb454339" />



<img width="2105" height="1562" alt="image" src="https://github.com/user-attachments/assets/e5f7720a-7e32-4a64-ae82-fd47927118e6" />


We Hash Rows, when we place



<img width="377" height="452" alt="image" src="https://github.com/user-attachments/assets/9b81e75d-5172-44f0-b71a-0aea8d70f32d" />



```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    // Function to solve N-Queens problem
    void solve(int col, vector<string>& board, int n,
               vector<int>& leftRow, vector<int>& upperDiagonal, vector<int>& lowerDiagonal,
               vector<vector<string>>& ans) {
        // If all queens are placed
        if (col == n) {
            ans.push_back(board);
            return;
        }

        // Iterate through all rows
        for (int row = 0; row < n; row++) {
            // Check if it's safe to place the queen
            if (leftRow[row] == 0 && lowerDiagonal[row + col] == 0 &&
                upperDiagonal[n - 1 + col - row] == 0) {

                // Place the queen
                board[row][col] = 'Q';

                // Mark the row and diagonals
                leftRow[row] = 1;
                lowerDiagonal[row + col] = 1;
                upperDiagonal[n - 1 + col - row] = 1;

                // Recurse to next column
                solve(col + 1, board, n, leftRow, upperDiagonal, lowerDiagonal, ans);

                // Backtrack and remove the queen
                board[row][col] = '.';
                leftRow[row] = 0;
                lowerDiagonal[row + col] = 0;
                upperDiagonal[n - 1 + col - row] = 0;
            }
        }
    }

    // Main function
    vector<vector<string>> solveNQueens(int n) {
        vector<vector<string>> ans;
        vector<string> board(n, string(n, '.'));
        vector<int> leftRow(n, 0), upperDiagonal(2 * n - 1, 0), lowerDiagonal(2 * n - 1, 0);
        solve(0, board, n, leftRow, upperDiagonal, lowerDiagonal, ans);
        return ans;
    }
};

int main() {
    Solution obj;
    int n = 4;
    vector<vector<string>> res = obj.solveNQueens(n);
    for (auto& board : res) {
        for (auto& row : board) {
            cout << row << "\n";
        }
        cout << "\n";
    }
    return 0;
}

```
