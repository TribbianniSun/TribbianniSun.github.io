# Leetcode_123 Best Time to Buy and Sell Stock III


Use **Dynamic Programming - State Machine** to solve Leetcode_123 Best Time to Buy and Sell Stock III
<!--more-->

## Problem Description [Leetcode 123](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/)


<p>

You are given an array prices where prices[i] is the price of a given stock on the ith day.

Find the maximum profit you can achieve. You may complete at most two transactions.

Note: You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

</p>

## Examples Test Cases [Leetcode 123](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/)

```

Input: prices = [3,3,5,0,0,3,1,4]
Output: 6
Explanation: Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.

```

```
Input: prices = [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are engaging multiple transactions at the same time. You must sell before buying again.
```



## Problem Solution [Leetcode 123](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/)

```cpp
class Solution {
public:
    int f[100050][5][5];
    
    int maxProfit(vector<int>& prices) {
        memset(f, -0x2f, sizeof f);
        int n = prices.size();

        // initialize all the starting state to be 0, starting from day i, and do no transaction before
        for(int i = 0; i <= n; i++){
            f[i][0][0] = 0;
        }
        for(int i = 1; i <= n; i++){
            int val = prices[i - 1];
            for(int j = 1; j <= 2; j++){
                f[i][j][0] = max(f[i-1][j][0], f[i-1][j][1] + val);
                f[i][j][1] = max(f[i-1][j][1], f[i-1][j-1][0] - val);
            }
        }
        int ret = 0;
        for(int i = 1; i <= 2; i++) ret = max(ret, f[n][i][0]);
        return ret;
    }
};
```
## Problem Remark 
- DP -> 
- initialie all the starting state f[i][0][0] to be 0 (meaning that no transaction before at day i, gaining zero profit)



