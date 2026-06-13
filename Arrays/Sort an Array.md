# Sort an Array

[LeetCode](https://leetcode.com/problems/sort-an-array/description/)

Using Merge Sort 

# Merge Sort

- Merge: Store elements of 2 lists(low->mid,mid+1->high) in temp in sorted manner, then replace elements from low->high in main array by these temp array elements which are sorted
- mergeSort: if low>=high return, else apply merge sort on left Half, then apply mergeSort on Right Half, and then merge Both (Happens in same main array)

```cpp
class Solution {
public:
    void merge(vector<int> &nums, int low,int mid,int high){
        int i=low,j=mid+1;
        vector<int> temp;
        while(i<=mid && j<=high){
            if(nums[i]<=nums[j]){
                temp.push_back(nums[i]);
                i++;
            }else{
                temp.push_back(nums[j]);
                j++;
            }
        }
        while(i<=mid){
            temp.push_back(nums[i]);
            i++;
        }
        while(j<=high){
            temp.push_back(nums[j]);
            j++;
        }
        for(int k=low;k<=high;k++){
            nums[k]=temp[k-low];
        }
    }
    void mergeSort(vector<int> &nums,int low,int high){
        if(low>=high) return;
        int mid=low+((high-low)/2);  // Can also do (low+high)/2;
        mergeSort(nums,low,mid);
        mergeSort(nums,mid+1,high);
        merge(nums,low,mid,high);

    }
    vector<int> sortArray(vector<int>& nums) {
        int high=nums.size()-1;
        int low=0;
        mergeSort(nums,low,high);
        return nums;
    }
};

```

| Algorithm  | TC         | SC   |
| ---------- | ---------- | ---- |
| Merge Sort | O(N log N) | O(N) |
| Heap Sort  | O(N log N) | O(1) |

But:
- Not stable
- More complex implementation
- Usually slower in practice than Merge Sort
