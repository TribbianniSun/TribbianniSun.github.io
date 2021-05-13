# Leetcode_309 Best Time to Buy and Sell Stock with Cooldown



Use **Dynamic Programming - State Machine** to solve Leetcode_309 Best Time to Buy and Sell Stock with Cooldown.
<!--more-->

## Problem Description [Leetcode 309](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

<p>

You are given an array prices where prices[i] is the price of a given stock on the ith day.

Find the maximum profit you can achieve. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times) with the following restrictions:

After you sell your stock, you cannot buy stock on the next day (i.e., cooldown one day).
Note: You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

</p>



## Examples Test Cases [Leetcode 309](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

```
Input: prices = [1,2,3,0,2]
Output: 3
Explanation: transactions = [buy, sell, cooldown, buy, sell]
```

## Problem Solution [Leetcode 309](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)



```cpp
class Solution {
public:
    int f[5010][3];
    int maxProfit(vector<int>& prices) {
        f[0][0] = 0;
        f[0][1] = f[0][2] = -2e9;
        int n = prices.size();
        for(int i = 1; i <= n; i++){
            int val = prices[i-1];
            f[i][0] = max(f[i-1][1], f[i-1][0]);
            f[i][1] = f[i-1][2] + val;
            f[i][2] = max(f[i-1][2], f[i-1][0] - val);
        }
        return max(f[n][0], f[n][1]);
    }
};
```
