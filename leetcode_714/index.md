# Leetcode_714 Best Time to Buy and Sell Stock with Transaction Fee


Use **Dynamic Programming - State Machine** to solve Leetcode_714 Best Time to Buy and Sell Stock with Transaction Fee.
<!--more-->

## Problem Description [Leetcode 714](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)

<p>

You are given an array prices where prices[i] is the price of a given stock on the ith day, and an integer fee representing a transaction fee.

Find the maximum profit you can achieve. You may complete as many transactions as you like, but you need to pay the transaction fee for each transaction.

Note: You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).



</p>



## Examples Test Cases [Leetcode 714](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)

```
Input: prices = [1,3,2,8,4,9], fee = 2
Output: 8
Explanation: The maximum profit can be achieved by:
- Buying at prices[0] = 1
- Selling at prices[3] = 8
- Buying at prices[4] = 4
- Selling at prices[5] = 9
The total profit is ((8 - 1) - 2) + ((9 - 4) - 2) = 8.
```

## Problem Solution [Leetcode 714](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)


```cpp
class Solution {
public:

    int f[100050][2];
    
    int maxProfit(vector<int>& prices, int fee) {
        f[0][0] = 0;
        f[0][1] = -2e9;
        for(int i = 1; i <= prices.size(); i++){
            int val = prices[i-1];
            f[i][0] = max(f[i-1][0], f[i-1][1] + val - fee);
            f[i][1] = max(f[i-1][1], f[i-1][0] - val);
        }
        return f[prices.size()][0];
    }
};
```



