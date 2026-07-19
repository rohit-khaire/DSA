# Flood Fill

[Leetcode](https://leetcode.com/problems/flood-fill/)

similar to Number of Islands

We are guven a 2D matrix with row and column, we need to go to that index and change the color of that element to newColor 

Also check if neighbours have same oldColor or not? If they have old color, then also change it to newColor

So, we need to goto given index and change the color of that element to newColor ans also change the colors of Neighbours if they are havinf oldColor.

# Approach - DFS


- Check if given element is already having newColor? If yes then return image as it is
- Create a copy of image, so that our input is not altered


```cpp
class Solution {
public:
    void dfs(vector<vector<int>> &copy,int row,int col,int oldColor, int newColor){
        if(row<0 || row>=copy.size() || col<0 || col>=copy[0].size() || copy[row][col]!=oldColor) return;
        copy[row][col]=newColor;
        dfs(copy,row-1,col,oldColor,newColor);
        dfs(copy,row+1,col,oldColor,newColor);
        dfs(copy,row,col-1,oldColor,newColor);
        dfs(copy,row,col+1,oldColor,newColor);
    }
    vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int color) {
        int val = image[sr][sc];
        if (val == color)
            return image;
        vector<vector<int>> copy=image;
        dfs(copy,sr,sc,val,color);
        return copy;
    }
};
```


