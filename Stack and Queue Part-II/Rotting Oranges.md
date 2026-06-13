# Rotting Oranges

Problem Statement: Given an m x n grid, where each cell has the following values :

2 - represents a rotten orange , 1 - represents a Fresh orange , 0 - represents an Empty Cell .

Every minute, if a fresh orange is adjacent to a rotten orange in 4-direction ( upward, downwards, right, and left ) it becomes rotten.

Return the minimum number of minutes required such that none of the cells has a Fresh Orange(All oranges are rotten). If it's not possible, return -1..


# Approach Very Simple, solved in first Attempt, just by understanding the Concept

The idea is that for each rotten orange, we will find how many fresh oranges there are in its 4 directions. If we find any fresh orange we will make it into a rotten orange. One rotten orange can rotten up to 4 fresh oranges present in its 4 directions. For this problem,  we will be using the **BFS ( Breadth-First Search )** technique.

- First check if given grid is empty? If yes then return 0;
- total will have total no. of oranges(fresh+rottten), count will be used to count no. of oranges rotten by us, time will be used to keep track of days/seconds Total time taken to rot all reachable oranges
- Have 1 Queue to keep track of rotten orange's indices pair<int,int> 
- Traverse all the elements in the grid using 2 loops => O(N^2) - Get total no. of oranges and push rotten oranges in Queue
  - If the current cell (i,j) is not empty then add it in total (total++)
  - If current cell is having Rotten Orange then push it's indices in the Queue
- Now at time 0, we have q.size() no. of rotten oranges, initialize a counter to count no. of rotten oranges
- Now we loop while our Queue is not empty
  - Queue contains no. of rotten oranges at this time, count+=q.size()
  - We loop for current q.size() (k times) (Means for each element of Queue at this time only)
      - For each element of Queue, we get rotten orange's indices from q.front() and we pop() the queue's front
      -  Look in 4 Directions of that indices, if there is fresh orange, then make it Rotten and push it in Queue
      -  k--
  - If our Queue is Not empty, then increment the time, as we will be performing the same for that incremented time(Like for 0 time it's done, now do the same for time 1, means remaining elements in Queue will take 1 second time)
- Now our Queue is empty, Now If our counted rotten oranges are equals to total, means all the oranges are rotten, so we can return the time taken or else we will return -1 as not all the oranges are rotten 

<br><br>

```cpp
class Solution {
public:
    int orangesRotting(vector<vector<int>>& grid) {
        if(grid.empty() || grid[0].empty()) return 0;
        int m=grid.size();
        int n=grid[0].size();

        queue<pair<int,int>> q; //Keep Track of Rotten Oranges

        int total=0; //Total is Total no. of oranges initially(fresh+rotten)
        int time=0;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(grid[i][j]!=0){ //Get total no. of oranges (fresh+rotten)
                    total+=1;
                }
                if(grid[i][j]==2){
                    q.push({i,j});  // Push Rotten Oranges
                }
            }
        }
        int count=0; //Now we can count how many oranges we are rottening, to match is it equals to Total
        //At time 0, we have rotten oranges in Q
        while(!q.empty()){
            int k=q.size(); //No. of oranges in Q at this time
            count+=k; //No. of oranges rotten till now
            while(k){ //Perform only for elements having same time
                int i=q.front().first;
                int j=q.front().second;
                //Got position of rotten orange as grid[i][j]
                q.pop();    
                // Look in 4 Directions
                if(i-1>=0){ //above row
                    if(grid[i-1][j] == 1){
                        grid[i-1][j]=2;
                        q.push({i-1,j});
                    }
                }
                if(i+1<m){ //below row
                    if(grid[i+1][j]==1){
                        grid[i+1][j]=2;
                        q.push({i+1,j});
                    }
                }
                if(j-1>=0){ //prev column
                    if(grid[i][j-1]==1){
                        grid[i][j-1]=2;
                        q.push({i,j-1});
                    }
                }
                if(j+1<n){ //after column
                    if(grid[i][j+1]==1){
                        grid[i][j+1]=2;
                        q.push({i,j+1});
                    }
                }
                k--; 
            }
            if(!q.empty()) time++;
        }
        return total==count?time:-1;
    }
};
```

TC=O(m×n) for getting total  + O(m×n) BFS Queue push and pop = O(2mn) = O(m×n)

SC = O(m×n)
