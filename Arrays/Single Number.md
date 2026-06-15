# Single Number 

Given a non-empty array of integers nums, every element appears twice except for one. Find that single one.

[LeetCode](https://leetcode.com/problems/single-number/description/)

# Brute Force

Hash all the numbers in Array with it's count and then traverse the Hash and get element whose count is 1

TC=O(2N) as N to hash all elements with their count and N for traversing the hash count to get count 1

SC=O(N) as extra hashing {value,count}

# OPTIMAL using XOR

**XOR (^)** works on bits like => IF bits are same THEN 0

XOR cancels duplicates like 

4^4 = 0

a^0 = a or 0^a =a

**We perform XOR on every element of Array** => a[0] ^ a[1] ^ a[2] ^ a[3]

Example:

[4,1,2,1,2]

If we do 4^1^2^1^2 = 1 cancels other one, 2 cancels other 2, so we get 4 = 4 <=ANS

```cpp
res = 4
res = 4^1 = 5
res = 5^2 = 7
res = 7^1 = 6 //1 cancels previous 1
res = 6^2 = 4 //2 cancels previous 2
```

The magic is that duplicates eventually meet and cancel:


```cpp
4 ^ 1 ^ 2 ^ 1 ^ 2
= 4 ^ (1 ^ 1) ^ (2 ^ 2)
= 4 ^ 0 ^ 0
= 4
```

CODE:

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int res=nums[0];
        for(int i=1;i<nums.size();i++){
            res=res^nums[i];
        }
        return res;
    }
};
```

TC=O(N) and SC=O(1)

