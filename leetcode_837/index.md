# Leetcode_837. New 21 Game



Use **sliding-window** to solve Leetcode_837. New 21 Game
<!--more-->


## Problem Solution [Leetcode 837. New 21 Game](https://leetcode.com/problems/new-21-game/)

```python
class Solution:
    def new21Game(self, n: int, k: int, maxPts: int) -> float:
        if(k == 0 or n >= k + maxPts):
            return 1
        dp = [0 for _ in range(n + 5)]
        dp[0] = 1.0
        running_sum = dp[0]
        for i in range(1, n + 5):
            dp[i] = running_sum / maxPts

            # if i >= k, the game is over
            if i < k:
                running_sum += dp[i]
            
            # maintain the sliding window of size k (fixed)
            if i >= maxPts:
                running_sum -= dp[i - maxPts]
        
        ret = 0
        for i in range(k, n + 1, 1):
            ret += dp[i]
        return ret
            
```


