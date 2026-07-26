# Permutations

[Leetcode](https://leetcode.com/problems/permutations/)

Find all the possible Permutations for a given array. Return a 2D vector of all the Permutations.

# Approach - Recursion

<img width="784" height="442" alt="image" src="https://github.com/user-attachments/assets/c4661622-5150-4ddb-bc76-cf1e5802d83d" />

We create a recursive function that takes nums array,index i,ans array as input

- if index(i) is >= arr.size(), we just add the array arr in answer as it's one Permutation, then return
- we make j=i and start a loop from j=i to N (For each number, we just swap current index with next numbers)
  - we swap arr[i] with arr[j], Now we got a new Number Like for 123 it's 123 & 213 & 321
  - recursive call => rec(arr,i+1,ans) , this will make it point to next index
  - again swap arr[i] with arr[j], so that we can get previous number again (This is done to form next number like from 123, we created 213, now we again make it 123, so that next number can be formed like 321)

<br>

```cpp
class Solution {
public:
    void rec(vector<int> arr,int i,vector<vector<int>> &ans){
        if(i>=arr.size()){
            ans.push_back(arr);
            return;
        }
        int j=i;
        while(j<arr.size()){
            swap(arr[i],arr[j]);
            rec(arr,i+1,ans);
            swap(arr[i],arr[j]); //back to normal
            j++;
        }
    }
    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> ans;
        rec(nums,0,ans);
        return ans;
    }
};
```
