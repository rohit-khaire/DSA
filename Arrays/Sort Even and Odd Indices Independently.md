# 2164. Sort Even and Odd Indices Independently

[LeetCode](https://leetcode.com/problems/sort-even-and-odd-indices-independently/description/)

Sort Even-indexed elements in ascending order & Odd-indexed elements in descending order.

# Brute Force 

Store even index and odd index in 2 different arrays and then sort both arrays and then put elements in original array.

# Optimal

As nums[i] is from 1 to 100 only, so create a frequency array of size 101 => Indexes = 0 to 100, we can use 1 to 100

Traverse even index in array nums, increase frequency of that numbers

Now traverse frequency array from 1 to 100, and just replace the nums[i] with frequency's index where frequency is != 0

Fill all frequency array's values by 0

Now traverse odd index in array nums, increase frequency of that numbers

Now access frequency array from last(100) index to 1, and wherever freq[i]!=0, that index is our required value to be places in nums array 

```cpp
class Solution {
public:
    vector<int> sortEvenOdd(vector<int>& nums) {
        vector<int> freq(101,0); //As values are from 1 to 100 only
        // Even-indexed elements in ascending order.
        // Odd-indexed elements in descending order.

        //Let's first sort even index elements to asc order
        for(int i=0;i<nums.size();i+=2){ //even index = 0,2,4,6,8
            freq[nums[i]]++;
        }
        int val=1;
        for(int i=0;i<nums.size();i+=2){
            //i is index of nums array
            while(val<100 && freq[val]==0) val++;
            nums[i]=val;
            freq[val]--;
        }

        //Now lets do for odd index of nums - desc order
        fill(freq.begin(),freq.end(),0);

        for(int i=1;i<nums.size();i+=2){ //odd index - 1,3,5,7,9
            freq[nums[i]]++;
        }
        val=100;
        for(int i=1;i<nums.size();i+=2){
            //i is index of nums array
            while(val>0 && freq[val]==0) val--;
            nums[i]=val;
            freq[val]--;
        }


        return nums;
    }
};
```


TC:O(N) And SC:O(1)
