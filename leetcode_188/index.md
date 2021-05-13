# Leetcode_188 Best Time to Buy and Sell Stock IV


Use **Dynamic Programming - State Machine** to solve Leetcode_188 Best Time to Buy and Sell Stock IV
<!--more-->

## Problem Description [Leetcode 188]https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/


<p>

You are given an integer array prices where prices[i] is the price of a given stock on the ith day, and an integer k.

Find the maximum profit you can achieve. You may complete at most k transactions.

Note: You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

</p>

## Examples Test Cases [Leetcode 188]https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/

```
Input: k = 2, prices = [2,4,1]
Output: 2
Explanation: Buy on day 1 (price = 2) and sell on day 2 (price = 4), profit = 4-2 = 2.
```

```
Input: k = 2, prices = [3,2,6,5,0,3]
Output: 7
Explanation: Buy on day 2 (price = 2) and sell on day 3 (price = 6), profit = 6-2 = 4. Then buy on day 5 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
```



## Problem Solution [Leetcode 188](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/)

```cpp
class Solution {
public:
    int f[1050][105][5];
    int maxProfit(int k, vector<int>& prices) {
        memset(f, -0x3f, sizeof f);
        int n = prices.size();
        for(int i = 0; i <= n; i++){
            f[i][0][0] = 0;
        }
        
        for(int i = 1; i <= n; i++){
            int val = prices[i-1];
            for(int j = 1; j <= k; j++){
                f[i][j][0] = max(f[i-1][j][0], f[i-1][j][1] + val);
                f[i][j][1] = max(f[i-1][j][1], f[i-1][j-1][0] - val);
            }
        }
        
        int ret = 0;
        for(int j = 1; j <= k; j++) ret = max(ret, f[n][j][0]);
        return ret;
    }
};
```
