# Search in a sorted 2D matrix

[LeetCode](https://leetcode.com/problems/search-a-2d-matrix/description/)


## Brute Force 

The extremely naive approach is to get the answer by checking all the elements of the given matrix. So, we will traverse the matrix and check every element if it is equal to the given ‘target’.


## Better ( Binary Search on Specific row only) Beats 100%

As all elese are sorted. So apply binary search only on specific row only where target element can be found.

If the target lies between the first and last element of the row, i (i.e. matrix[i][0] <= target && target <= matrix[i][m-1]), we can conclude that the target might be present in that specific row.

Once we locate the potentially relevant row containing the 'target', we need to confirm its presence. To accomplish this, we will utilize the Binary search algorithm, effectively reducing the time complexity.

```
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m = matrix.size();
        int n = matrix[0].size();

        for(int i=0;i<m;i++){
            if(target >= matrix[i][0] && target<= matrix[i][n-1]){
                int low =0, high=n-1, mid;
                while(low<=high){
                    mid = (low+high)/2;
                    if(matrix[i][mid] == target){
                        return true;
                    }
                    else if(target > matrix[i][mid]){
                        low = mid+1;
                    }
                    else if(target < matrix[i][mid]){
                        high = mid-1;
                    }
                }
                
            }
        }
        return false;
    }
};
```

TC = O(n * logm )

SC = O(1)

## Optimal ( Treat 2D Matrix as 1D and apply binary search ) Beats 100%


<img width="616" height="338" alt="image" src="https://github.com/user-attachments/assets/6d6713e2-13cb-4ffc-bb13-6d1a274a4a7f" />

<br>

If we flatten the given 2D matrix into a 1D array, that 1D array would also be sorted. By running binary search on this flattened version, we could quickly check if the element exists.

But actually flattening the matrix takes extra time and memory, which makes it inefficient. Instead, we can simulate the flattening without creating a new array. The trick is to directly map a 1D index into the corresponding row and column of the 2D matrix.

To do this mapping, if there are `m` columns in the matrix and the index is `i`, then: <br>
Row = i / m, Column = i % m. <br>

So instead of working on the 2D matrix directly, we pretend it’s a sorted 1D array of length (rows × columns), and apply binary search on this imaginary array.

Start with two pointers: one at the first index of the imaginary 1D array, and the other at the last index. <br>
While the first pointer does not cross the last: <br>
Find the middle index between the two pointers.

Convert this middle index into a row and column of the original 2D matrix.

If the element at that position matches the target, return true (element found).

If the element is smaller than the target, discard the left half and continue searching in the right half.

If the element is larger than the target, discard the right half and continue searching in the left half.

If the search ends without finding the element, return false (element not present in the matrix).



```
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& arr, int target) {
        int m = arr.size();
        int n = arr[0].size();
        int low=0, high = (n*m)-1,mid,row,col;
        while(low<=high){
            mid = (low+high)/2; //mid index in 1D
            row = mid/n;
            col = mid%n;
            if(target == arr[row][col]){
                return true;
            }
            else if(target> arr[row][col]){
                low = mid + 1;
            }
            else{
                high = mid-1;
            }

        }
        return false;
    }
};
```

TC = O(log m*n)

SC = O(1)
