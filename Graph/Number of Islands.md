# Number of Islands

[LeetCode](https://leetcode.com/problems/number-of-islands/description/)

Just count all the numbers of islands

# Approach

- Iterate through each element of grid
- if current element is '1', then make all the elements in 4 directions (left,right,up,down) as 0s (visited)

```cpp
class Solution {
public:
    void dfs(vector<vector<char>> &g,int i,int j){ //mark all consicuties 1 to zeros, mark all the connected 1s to 0 in all the four directions 
        int m = g.size(); 
        int n = g[0].size();
        if(i<0 || j<0 || i>=m || j>=n || g[i][j]=='0') return;
        g[i][j]='0';
        dfs(g,i-1,j);
        dfs(g,i+1,j);
        dfs(g,i,j-1);
        dfs(g,i,j+1);
    }
    int numIslands(vector<vector<char>>& grid) {
        int m = grid.size();
        int n = grid[0].size();
        int islands=0;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
               if(grid[i][j]=='1'){
                islands++;
                dfs(grid,i,j);
               }
            }
        }
        return islands;
    }
};
```
