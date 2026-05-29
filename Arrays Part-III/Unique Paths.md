# Unique Path

[LeetCode](https://leetcode.com/problems/unique-paths/)

Problem Statement: Given two integers m and n, representing the number of rows and columns of a 2d array named matrix. Return the number of unique ways to go from the top-left cell (matrix[0][0]) to the bottom-right cell (matrix[m-1][n-1]).

Movement is allowed only in two directions from a cell: right and bottom.

But I will go from [m-1][n-1] to [0][0] , with directions up and left only

*Similar Concepts and Notes and Code are in DSA Notebook*

## Without Memoization (without dp grid ( Exceeds Time Limit ) Purely recursion

```
class Solution {
public:
    int f(int row, int col){
        // start from m-1 , n-1
        if(row==0 && col==0) return 1;
        if(row<0 || col<0) return 0;
        int left = f(row,col-1);
        int up = f(row-1,col);
        return left+up;
    }
    int uniquePaths(int m, int n) {
        int res = f(m-1,n-1);
        return res;
    }
};
```


## With Recursion + Memoization (extra dp grid for storing)

So that same computaion doesn't needs to be done again and again. Similar solved and Concepts are in Notebook.

Declare a dp[] array of size [m][n], where m and n are the dimensions of the grid. This array stores the results of subproblems, where dp[i][j] represents the total number of ways to reach from (0,0) to (i,j).

Initially, fill the dp array with -1 to indicate that no subproblem has been solved yet.

While encountering an overlapping subproblem, check if the value in dp[i][j] is not -1. If the value is not -1, it means this subproblem has already been solved, and you can directly return the stored value from the dp array instead of recalculating it.

Whenever a subproblem is encountered and it is not solved yet (i.e., the value at dp[i][j] is -1), calculate the value of the subproblem and store it in the dp array for future reference. This ensures that future overlapping subproblems can be solved in constant time by retrieving the value from the array.

<img width="364" height="336" alt="image" src="https://github.com/user-attachments/assets/f28c7f82-ca3d-4c96-9e1f-a61d1a59b9cc" />

<br>

```
class Solution {
public:
    int f(int row, int col, vector<vector<int>> &dp){
        // start from m-1 , n-1
        if(row==0 && col==0) return 1;
        if(row<0 || col<0) return 0;
        if(dp[row][col] != -1) return dp[row][col];
        int left = f(row,col-1,dp);
        int up = f(row-1,col,dp);
        return dp[row][col]=left+up;
    }
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m,vector<int>(n,-1));
        int res = f(m-1,n-1, dp);
        return res;
    }
};
```

**TC = O(m*n)  and SC = O(m*n + m)**

## Using Tabulation ( No recursion, but with dp grid )

Declare a dp[] array of size [m][n], where m and n represent the number of rows and columns of the grid, respectively. The dp[i][j] stores the total number of ways to reach from the start (0,0) to the cell (i,j).

Set the base case: As per the recursive approach, dp[0][0] is 1, indicating there is only one way to reach the starting position. So, initialize dp[0][0] = 1.

Use two nested loops to fill the dp array iteratively. The outer loop iterates through rows (i from 0 to m-1), and the inner loop iterates through columns (j from 0 to n-1).

For each cell dp[i][j], calculate the number of ways to reach it from the top (dp[i-1][j]) and from the left (dp[i][j-1]). Add the values of dp[i-1][j] and dp[i][j-1] to get the total number of ways to reach dp[i][j].

As the question asks for the total number of ways, update dp[i][j] as the sum of dp[i-1][j] (ways from above) and dp[i][j-1] (ways from left).

Once all cells are processed, the last element dp[m-1][n-1] will contain the total number of ways to reach the destination (bottom-right corner) of the grid. Return this value as the result after the bottom-up computation.


```
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m,vector<int>(n,0));
        // Store in dp, no. of paths from [0][0] to [i][j]
        dp[0][0] = 1; // one way to reach from itself to itself
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(i-1 >= 0 ) dp[i][j] += dp[i-1][j];
                if(j-1 >= 0 ) dp[i][j] += dp[i][j-1];
            }
        }
        return dp[m-1][n-1];

    }
```

**TC = O(m*n) and SC = O(m*n)**


# Space Optimized Solution ( Instead of using whole dp grid, only used 2 vectors)

**No recursion or no whole dp grid**

Instead of using the whole dp grid, we can use a single array for storing vals and one array for computaion.

Likewise topic's notes are in DSA Notebook.

This reduced space and provides *100% Beating* Solution

* Algo:

Observe the relationship obtained in the tabulation approach: dp[i][j] = dp[i-1][j] + dp[i][j-1]. We notice that to calculate dp[i][j], we only need the values from the previous row and the current row. This allows us to optimize the space usage.

Instead of maintaining the entire 2D dp array, we can use two arrays, one for the current row (let's call it temp) and one for the previous row (let's call it prev).

Initially, initialize the prev array to all zeros to represent the starting point. The temp array will hold the current row's values during the iteration.

For each row, use the prev array (representing the previous row) and the temp array (representing the current row) to compute the values of dp[i][j].

After processing the current row, set prev to be equal to temp, so that in the next iteration, prev will represent the previous row, and temp will be ready to hold the new row's values.

At the end of the process, prev[n-1] will store the final result, which contains the total number of ways to reach the destination in the grid. This provides the answer in a space-efficient manner using only two rows.


```cpp
    int uniquePaths(int m, int n) {
        vector<int> prev(n,1);
        // Store in dp, no. of paths from [0][0] to [i][j]
        // one way to reach from itself to itself
        for(int i=1;i<m;i++){
            vector<int> temp(n,0);
            for(int j=0;j<n;j++){
                if(i-1 >= 0 ) temp[j] += prev[j];
                if(j-1 >= 0 ) temp[j] += temp[j-1];
            }
            prev = temp;
        }
        return prev[n-1];

    }
```

**TC = m*n and SC=2n**


Solution at 12:19 AM 🕛, that too with the efforts of whole dayyyy, Now I desrve sleeepppp
