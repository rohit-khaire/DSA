# Four Sum 

[LeetCode](https://leetcode.com/problems/4sum/)

Problem Statement: Given an array of N integers, your task is to find unique quads that add up to give a target value. In short, you need to return an array of all the unique quadruplets [arr[a], arr[b], arr[c], arr[d]] such that their sum is equal to a given target.

Note: a, b, c and d are also distinct and lies between 0 to n-1 (both inclusive).

## Brute Force 

Using 4 loops: 

- Create a set to keep only unique groups of four numbers. 

- Use the first loop from the start of the array to the end to choose the first number. (i=0 -> n)

- Inside it, run a second loop starting from the next position to choose the second number.(j=i+1)

- Then, run a third loop starting from the next position after the second number to choose the third number.(k=j+1)
 
- Finally, run a fourth loop starting from the next position after the third number to choose the fourth number.(l=k+1)
 
- Check if the total of these four numbers equals the target value. (target == sum)
 
- If yes, arrange the four numbers in order and add them to the set. (sort->insert)
 
- Once all loops are done, return the set as a list of unique groups of four numbers.(return set)


```cpp
class Solution {
public:
    // Function to find quadruplets with sum = target
    vector<vector<int>> fourSum(vector<int>& arr, int target) {
        // Get size of array
        int n = arr.size();
        // Use set to avoid duplicate quadruplets
        set<vector<int>> st;

        // First loop - pick first element
        for (int i = 0; i < n; i++) {
            // Second loop - pick second element
            for (int j = i + 1; j < n; j++) {
                // Third loop - pick third element
                for (int k = j + 1; k < n; k++) {
                    // Fourth loop - pick fourth element
                    for (int l = k + 1; l < n; l++) {
                        // Calculate sum of four chosen numbers
                        long long sum = (long long)arr[i] + arr[j] + arr[k] + arr[l];
                        // Check if sum matches target
                        if (sum == target) {
                            // Store quadruplet in sorted order
                            vector<int> temp = {arr[i], arr[j], arr[k], arr[l]};
                            sort(temp.begin(), temp.end());
                            // Insert into set to ensure uniqueness
                            st.insert(temp);
                        }
                    }
                }
            }
        }
        // Convert set into vector of quadruplets
        return vector<vector<int>>(st.begin(), st.end());
    }
};
```


**TC=O(n^4) * sorting of 4 eles O(1) * Set insertion → O(log M)** where M is the number of quadruplets already in the set.

In the worst case, M can be n^4.

Overall TC = O(n^4 * log(n^4)) 

log n^4 = 4 log(n) -> O(4 * n^4 * log(n) ) = *O(n^4 * log(n)*

log is set insertion cost

**Space Complexity: O( no. of the unique triplets) as we are using a set data structure and a list to store the triplets.**

In worst case it's O(n^2)
<br><br>

## Better Solution

- Create a set to keep only unique groups of four numbers. (set<vector<int>>) Set of int vector
- Run the first loop from the start to the end of the array to pick the first number.(i=0->n)
- Inside it, run the second loop from the next position to pick the second number.(j=i+1->n)
- Before starting the third loop, make a HashSet to keep track of numbers between the second and third positions. unordered_set<int> seen; (It will be later used to find more variable)
- Run the third loop from the next position after the second number to the end of the array to pick the third number.(k=j+1->n)
- Find the fourth number by subtracting the total of the first three numbers from the target value.(more=target-sum)
- If this fourth number is already in the HashSet, arrange all four numbers in order and add them to the set.(sort->insert to result)
- Add the current third number to the HashSet (only numbers between the second and third loops are stored). So that can be found later.
- After all loops finish, return the set as a list of unique groups of four numbers. (return)

```cpp
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        set<vector<int>> res; //end result
        int n= nums.size();
        for(int i=0;i<n;i++){
            for(int j=i+1;j<n;j++){
                unordered_set<int> temp; //stores eles between j and k
                for(int k=j+1;k<n;k++){
                    long long more = (long long)target - (long long)nums[i] - (long long)nums[j] - (long long)nums[k]; //as computation can be very big
                    if(more >= INT_MIN && more <= INT_MAX && temp.count((int)more)){  // If more is int and exists in temp
                        vector<int> sortFour = {nums[i],nums[j],nums[k],(int)more};  //Make quad
                        sort(sortFour.begin(),sortFour.end());  //Sort and Store it as result
                        res.insert(sortFour);
                    }
                    temp.insert((int)nums[k]);  //Put current val of nums[k] in temp to represent as it exists in between j and k, so that more can be found
                }
            }
        }
        return vector<vector<int>>(res.begin(),res.end());   //Type cast set to vector of int vector 
    }
};
```
