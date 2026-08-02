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

