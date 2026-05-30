# Reverse Pairs : Merge Sort + Two Pointer

[LeetCode](https://leetcode.com/problems/reverse-pairs/)

**Logic is in DSA Notebook**

Problem Statement: Given an array of numbers, you need to return the count of reverse pairs. <br> Reverse Pairs are those pairs where i<j and arr[i]>2*arr[j].

## Brute Force : Time Limit Exceeds for large input

The naive approach is pretty straightforward. We will use nested loops to generate all possible pairs. We know index i must be smaller than index j. So, we will fix i at one index at a time through a loop, and with another loop, we will check(the condition a[i] > 2*a[j]) the elements from index i+1 to N-1  if they can form a pair with a[i].

Note: For a better understanding of intuition, please watch the video at the bottom of the page.

Approach:

The steps are as follows:

First, we will run a loop(say i) from 0 to N-1 to select the a[i]. 

As index j should be greater than index i, inside loop i, we will run another loop i.e. j from i+1 to N-1, and select the element a[j].

Inside this second loop, we will check if a[i] > 2*a[j] i.e. if a[i] and a[j] can be a pair. If they satisfy the condition, we will increase the count by 1.

Finally, we will return the count i.e. the number of such pairs.

```cpp
class Solution {
public:
    int reversePairs(vector<int>& arr) {
        int n= arr.size();
        int cnt =0;
        for(int i=0;i<=n-2;i++){
            for(int j=i+1;j<n;j++){
                if((long long)arr[i]>2LL*arr[j]) cnt++;
            }
        }
        return cnt;
    }
};
```

**But this gives Time Limit Exceed Error**

**TC = O(N^2) and SC=O(1)**

> *For n = 50,000, that's about 1.25 billion comparisons, which will definitely TLE (Time Limit Exceed)*

> If I somehow keep the left half sorted and right half sorted, then for every left element I can find all valid right elements in one pass using two pointers, one on left sorted array and second on right sorted array.


# Optimal : Merge Sort + Two Pointers

**Merge Sort because it naturally creates two sorted halves.**

Here, our approach will be to check, for every element in the sorted left half(sorted), how many elements in the right half(also sorted) can make a pair. Let’s try to understand, using the following example:

<img width="671" height="313" alt="image" src="https://github.com/user-attachments/assets/12eff520-1e31-499f-8b5a-d049f3ad0a75" />
<br>

We check for every element in arr1[] what are the no. of elements in arr2[] which are arr1[i]<2*arr2[j] 

## Easy Understanding

Memory Trick

Remember:

Divide → Count → Merge

Because to count reverse pairs, we need:

Left Half Sorted and 

Right Half Sorted

but not necessarily the whole array sorted.

After counting, merge them.

```cpp
1. Merge Sort divides array.

2. Left recursion gives sorted left half.

3. Right recursion gives sorted right half.

4. Use two pointers to count:
      arr[i] > 2*arr[j]

5. Since both halves are sorted,
   right pointer never moves back. Whatever is satisfied in arr2[] for arr1[1], that much of part will be satisfied for arr[1] to arr[mid]
    as All the part from low to mid is in sorted manner
Ex. arr1[] ={6,12,19,22}
arr2[]={4,5,7,8}
So for arr1[1] = 12 => in arr2 4,5 is satified

So for next eles in arr1 like for 19 and 22 => 4,5 is satisfied

6. Count all cross pairs.
while(right<=high && arr[left] > 2LL*arr[right])
    right++;

count += right - (mid+1);

right reached first invalid position ( arr[left] !> 2*arr[right] )

Therefore all previous right elements
are valid reverse pairs.


7. Merge both halves.

8. Return:
   count = leftCount + rightCount + crossCount
```
<br>

Note: This process will work because arr1[1] will always be greater than arr1[0] which concludes if arr2[0] and arr2[1] are making a pair with arr1[0], they will obviously make pairs with a number greater than arr1[0] i.e. arr1[1].

Thus before the merge step in the merge sort algorithm, we will calculate the total number of pairs each time.

<br>

```cpp
class Solution {
public:
    void merge(vector<int> &arr, int low, int mid, int high){
        int left=low;
        int right=mid+1;
        vector<int> temp;
        while(left<=mid && right<=high){
            if(arr[left]<=arr[right]){
                temp.push_back(arr[left]);
                left++;
            }else{
                temp.push_back(arr[right]);
                right++;
            }
        }
        while(left<=mid){
            temp.push_back(arr[left]);
            left++;
        }
        while(right<=high){
            temp.push_back(arr[right]);
            right++;
        }
        for(int i=0;i<temp.size();i++){
            arr[low+i]=temp[i];
        }
    }
    int countPairs(vector<int> &arr, int low, int mid, int high){
        //treating arr as 2 different sorted arrays 1.low to mid and 2.mid+1 to high
        int cnt=0;
        int left=low, right=mid+1;
        while(left<=mid){
            while(right<=high && arr[left]>2LL*arr[right]){ right++;}
            left++;
            cnt+= (right-(mid+1));
        }
        return cnt;
    }
    int mergeSort(vector<int> &arr, int low,int mid, int high){
        int cnt=0;
        if(low>=high) return cnt;
        cnt += mergeSort(arr,low,(low+mid)/2,mid);  //Divide in parts
        cnt += mergeSort(arr,mid+1,(mid+1+high)/2,high); 
        cnt += countPairs(arr, low, mid, high);
        merge(arr,low, mid, high);
        return cnt;

    }
    int reversePairs(vector<int>& nums) {
        int n=nums.size();
        int low=0;
        int high=n-1;
        int mid=n/2;
        return mergeSort(nums, low, mid,high);
        
    }
};
```


Approach:

The steps are basically the same as they are in the case of the merge sort algorithm. The change will be just in the mergeSort() function:

In order to count the number of pairs, we will keep a count variable, cnt, initialized to 0 beforehand inside the mergeSort().

We will add the numbers returned by the previous mergeSort() calls.

Before the merge step, we will count the number of pairs using a function, named countPairs().

We need to remember that the left half starts from low and ends at mid, and the right half starts from mid+1 and ends at high.

The steps of the countPairs() function will be as follows:

We will declare a variable, cnt, initialized with 0.

We will run a loop from low to mid, to select an element at a time from the left half.

Inside that loop, we will use another loop to check how many elements from the right half can make a pair.

Lastly, we will add the total number of elements i.e. (right-(mid+1)) (where right = current index), to the cnt and return it.

> We use Merge Sort because after recursion both halves become sorted. For each element in the left half, I move a pointer in the right half while arr[i] > 2*arr[j]. Since both halves are sorted, the right pointer never moves backward, giving O(N) counting per merge step. Then I merge the two halves. Total complexity becomes O(N log N).


**TC = O(N log N) and SC = O(N)**

Time Complexity: O(2N*logN), Inside the mergeSort() we call merge() and countPairs() except mergeSort() itself. Now, inside the function countPairs(), though we are running a nested loop, we are actually iterating the left half once and the right half once in total. That is why, the time complexity is O(N). And the merge() function also takes O(N). The mergeSort() takes O(logN) time complexity. Therefore, the overall time complexity will be O(logN * (N+N)) = O(2N*logN).

Space Complexity: O(N), as in the merge sort We use a temporary array to store elements in sorted order.
