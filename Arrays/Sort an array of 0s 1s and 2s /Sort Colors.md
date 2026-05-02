# Sort an array of 0s 1s and 2s / Sort Colors

[Sort Colors](https://leetcode.com/problems/sort-colors/description/)

Array containing random values : 1s, 2s , 3s

These are colors represented in the form of Number

## Brute Force

Use any sorting algo, like Merge Sort which can take TC of (N logN) and SC of N

## Better Solution

Keep 3 variables for count of 0s and 1s and 2s, and increase it, 

perform 1 iteration of counting and another iteration of manually filling/overwritting the array with the no.s 0,1,2s

**TC = O(2N) and SC= O(1)**

## OPTIMAL SOLUTION

**Dutch National Flag Algorithm**

3 Pointers: low, mid, high

[0 to low-1] = 0   (Extreme Left)

[low to mid-1] = 1

**[mid to high] = 0s,1s,2s randomly in unsorted way**

[high+1 to n-1] = 2 (Extereme Right)

<img width="417" height="170" alt="image" src="https://github.com/user-attachments/assets/c66ee46a-3415-4dfa-9138-d38249e65cc2" />

*Logic:*

While Visualizing, Imagine it as :

<img width="1398" height="190" alt="image" src="https://github.com/user-attachments/assets/7b8859de-b748-4163-ba64-834e4a9b1aa8" />

<br>

mid to high => Unsorted random no.s

Start with low, mid pointing to index 0 and high pointing to n-1 index

Now unsorted array is mid to high

```
0  1  2  3  4  5  6  7  8   <-Indices
^                       ^
|                       |
low,mid                high
```

<br>

```
arr[mid] == 0 {
  swap(arr[mid],arr[low]);
  low++;
  mid++; //as mid-1 was already having 1 and mid swapped by low (i.e. 1) so now can go ahead
}

arr[mid] == 1 {
  mid++;
}

arr[mid] == 2 {
  swap(arr[mid], arr[high] );
  high--;
  check arr[mid] again
}
```

<br>
<br>
CODE:

```
class Solution {
public:
    vector<int> sortColors(vector<int>& arr) {
        int n = arr.size();
        int low = 0;
        int mid=0;
        int high = n-1;

        while(mid<=high){
            if(arr[mid]==0){
                swap(arr[mid],arr[low]);
                low++;
                mid++;
            }
            else if(arr[mid]==1){
                mid++;
            }
            else if(arr[mid]==2){
                swap(arr[mid],arr[high]);
                high--;
            }

        }

        return arr;
    }
};
```

**It's shrinking like mid and high are coming closer, TC O(n) and SC O(1)**
