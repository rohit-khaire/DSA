# Merge Sorted Arrays Without Extra Space

[LeetCode](https://leetcode.com/problems/merge-sorted-array/description/)

## Brute Force ( With Extra Array)

Keep 2 pointers, one on array num1 and other on array num2

check that which is smaller and then put the smaller in the new array, move and repeat

If you reach the end of any of the arrays (num1 or num2), then put the remaining values from the other array directly into the new array

Then put the values of new Array into the arrays num1 and num2

## Optimal Solution (1) without Extra Space

```
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int left = m-1;
        int right = 0;
        while(left>=0 && right<=n-1){
            if(left>right){
                swap(nums1[left],nums2[right]);
                left--;
                right--;
            }
            else{
                break;
            }
        }
        sort(nums1,nums1+m);
        sort(nums2,nums2+n);
    }
};
```

Keep pointer (left) on end of nums1 array and other pointer (right) on starting of nums2 array

Now check if left wali value if greater than right wali value, then swap them

left-- and right++

if anywhere left<=right, break, as both the arrays were sorted so values from 0 to left are more smallers in nums1 array

Then sort both the arrays, and then done, you have sorted vals in arrays nums1 and nums2

TC = O(min(m,n)) + 

O(nlogn) + O(nlogn) // Sorting

SC = O(1)

## Very basic solution if you keep solution in 1st array ( Beats 100% )

```
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        for(int i=m;i<m+n;i++){
            nums1[i] = nums2[i-m];
        }
        sort(nums1.begin(), nums1.end());
    }
};
```

TC = O((m+n) log(m+n))

*There is another solution with shell sort in Video*


# Most Optimal & Best to Use

<img width="596" height="136" alt="image" src="https://github.com/user-attachments/assets/c387630d-aa19-41da-a2e9-8d88dd2c5680" />

<br>

```
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int i = m - 1;  //end index of nums1, before 0s
        int j = n - 1;  //end index of nums2
        int k = m + n - 1; //end index of nums1 array, after 0s, currently pointing to last o in nums1
        
        while(j>=0){
            if(i>=0 && nums1[i]>nums2[j]){
                nums1[k]=nums1[i];
                k--;
                i--;
            }
            else{
                nums1[k]=nums2[j];
                k--;
                j--;
            }
        }
    }
};
```

Logic:

K chya position vr values put karaichey, put it at very last of nums1

i la put on position on m-1 ( from m , 0s starts)

j la end of nums2 

Now, compare kr nums1[i] and nums2[j] and put max on Kth place

nums1[k] = max( nums[i] , nums[j] )

jyala put kelay tyala minus kr, if taken value at Kth position is from nums1 then i--, else j--

## Simple Dry Run of it

Example:

```cpp id="q7hh0j"
nums1 = [1,2,3,0,0,0]
m = 3

nums2 = [2,5,6]
n = 3
```

Initial pointers:

```cpp id="5thm67"
i = 2   -> nums1[i] = 3
j = 2   -> nums2[j] = 6
k = 5
```

---

# Dry Run

## Step 1

Compare:

```cpp id="lc97cr"
3 vs 6
```

6 is bigger → place at `k`

```text
[ 1 | 2 | 3 | 0 | 0 | 6 ]
                      ↑
                      k
```

Move:

```cpp id="4o88u9"
j--
k--
```

---

## Step 2

Compare:

```cpp id="3qxky1"
3 vs 5
```

5 is bigger

```text
[ 1 | 2 | 3 | 0 | 5 | 6 ]
                  ↑
                  k
```

Move:

```cpp id="6ls7iw"
j--
k--
```

---

## Step 3

Compare:

```
3 vs 2
```

3 is bigger

```text
[ 1 | 2 | 3 | 3 | 5 | 6 ]
              ↑
              k
```

Move:

```
i--
k--
```

---

## Step 4

Compare:

```
2 vs 2
```

Else part runs → place nums2[j]

```text
[ 1 | 2 | 2 | 3 | 5 | 6 ]
          ↑
          k
```

Move:

```
j--
k--
```

---

## Step 5

Now:

```
j < 0
```

Stop.

Final:

```text
[ 1 | 2 | 2 | 3 | 5 | 6 ]
```

---

# Why Start From Back?

Because front positions already contain valid elements.

If we start from front:

```text
[1 2 3 0 0 0]
```

we may overwrite important values.

So we safely fill empty space from the end.

---

# Time Complexity

Each element is visited once:

```cpp id="2pcw3n"
O(m+n)
```

---

# Space Complexity

No extra array used:

```cpp id="rjlwmj"
O(1)
```


