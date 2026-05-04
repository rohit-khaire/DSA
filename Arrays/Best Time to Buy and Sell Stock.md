# Best Time to Buy and Sell Stock

[LeetCode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/)

Decide a Day to 

Buy Stock 

Sell Stock

Maximize The Profit ( Selling Price - Buying Price )

So to sell, you first needs to buy the stock, then only you can sell it.

Buy and Selling can only be done once, so remember to have maximum profit.

**If you are selling on ith Day then You buy on the minimum price from 0 to (i-1)**

Logic:

prices = [7,1,5,3,6,4]

You everytime check that for ith day, from 0 to i-1 array what was minimum price available(using variable minim), and if today's price-minm price is greater than maxProfit then take that profit

Assume maxProfit=0, and assume currently prices[0] is *Minimum*

Start a loop from index 1 to n-1 with variable i

Calculate cost(can be profit or loss) by using *prices[i]-minimum* (today's price - lowest price from left array)

Check that cost with maxProfit and **Select the Maximum as maxProfit** maxProfit = max(cost,maxProfit)

**Before moving further** check that is current day is having minimum price than the Variable minimum : minm= min(minim,prices[i])

Yes current day is having lower price than Variable minim, then today is the best price to buy




## Code:

```
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n=prices.size();
        int maxProfit=0;
        int minm=prices[0];
        for(int i=1;i<n;i++){
            int cost = prices[i]-minm;
            maxProfit = max(maxProfit,cost);
            minm = min(minm, prices[i]);
        }
        return maxProfit;
    }
};
```
