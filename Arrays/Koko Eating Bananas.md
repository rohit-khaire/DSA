# Koko Eating Bananas

[Leetcode](https://leetcode.com/problems/koko-eating-bananas/)

We have a Array with bananas in it. We need a minimum value of ``k`` such that eating k bananas per hour will take 


Brute and Optimal, both have same approach, bas Brute is using O(N) search and Optimal is using Binary Search O(logN)

# Brute Force

Start with 1 and increment one by one until max value from array <- This loop is value of K

Each time check if with this K, how much time it will take to eat all bananas

If time taken is less than or equal to required time(H), return k


# Optimal Approach

<img width="648" height="379" alt="image" src="https://github.com/user-attachments/assets/a3f97b4b-38c3-4067-909b-4614469affe8" />


The low always end up on opposite polarity, from where possible k starts, and high ends up at the very last Not possible K.

So if you don't have ans variable, then also it's fine as at the end ans is low.


> Note that Binary search is happening on possible K which ranges from 1 to max(eleInArray)


- Have a function that calculates Total time taken if Coco can eat K number of bananas in an Hour, we take ceil of Time like for 2.5 hours we take 3 hours
- Using loop from 0 to N, get maximum element in the array as Maxi
- Now 1 is our lower end and maxi is high => 1,2,3,......,maxi
- low points to 1 and high points to maxi
- now we apply binary search and get the mid
- we check the TimeTaken if Mid is our K, if it satisfies (TimeTaken<=h), we need left half
- Else we take right half
- Eventually when low passes high, our low is at minimum value that can help Coco => Coco can eat that much of bananas in an hour, so that it can finish all the bananas in H hours
- All the values from 1 to new high are not possible values (Time exceeds H)
- and all the values from low are possible values of k, and low is the lowest possible value

```cpp
class Solution {
public:
    long long eatingKbananaPerHour(vector<int> &nums,int k){
        long long totalTimeTaken=0;
        for(int i=0;i<nums.size();i++){
            totalTimeTaken+=ceil((double)nums[i]/k); //for 3/2=1.5 we take it as 2
        }
        return totalTimeTaken;
    }
    int minEatingSpeed(vector<int>& piles, int h) {
        int n =piles.size();
        int maxi=0;
        for(int i=0;i<n;i++){
            maxi=max(maxi,piles[i]);
        }
        //Answer exists from 1 to maxi, but we need minimum value that is <=h;
        // Brute: Iterate from 1 to maxi
        // Optimal: Binary search on 1 to maxi
        // Also, maxi is the (our end) for answer (so that range is limited), but numbers>maxi are also answer, but we need minimum, so we are limmiting range from 1 to maxi
        int low=1;
        int high=maxi;
        while(low<=high){
            int mid = low + ((high-low)/2);
            long long totalTimeTaken = eatingKbananaPerHour(piles,mid);
            if(totalTimeTaken<=h){
                //current mid value is also our answer, but we need minimum
                //hence we can also have ans variable here which can store minimum value of ans (mid)
                high=mid-1;
            }else{
                //answer is in right half
                low=mid+1;
            }
        }
        return low;

    }
};
```

