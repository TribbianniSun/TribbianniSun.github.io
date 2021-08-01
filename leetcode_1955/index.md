# Leetcode_1955 Count Number of Special Subsequences



Use **dp** to solve Leetcode_1955 Count Number of Special Subsequences
<!--more-->

```python
class Solution:
    def countSpecialSubsequences(self, nums: List[int]) -> int:
        ret = 0
        n = len(nums)
        mod = int(1e9 + 7)
        dp = [[0 for _ in range(4)] for _ in range(n + 5)]
        for i in range(1, n + 1, 1):
            v = nums[i - 1]
            dp[i][0] = dp[i-1][0]
            dp[i][1] = dp[i-1][1]
            dp[i][2] = dp[i-1][2]
            if(v == 0):
                dp[i][0] = (dp[i][0] + dp[i][0] + 1) % mod
            elif v == 1:
                dp[i][1] = (dp[i - 1][0] + dp[i][1] + dp[i][1]) % mod
            elif v == 2:
                dp[i][2] = (dp[i - 1][1] + dp[i][2] + dp[i][2]) % mod
            
        return dp[n][2]
```
