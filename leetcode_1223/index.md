# Leetcode_1223 Dice Roll Simulation



Use **Dynamic Programming** to solve Leetcode_1223 - Dice Roll Simulation
<!--more-->



## Problem Solution [1223. Dice Roll Simulation](https://leetcode.com/problems/dice-roll-simulation/)

```cpp
class Solution {
public:
    int MOD = 1e9 + 7;
    
    // dp[i][j][k] last is j, roll i times, consecutive combo is k
    
    long long dp[5005][6][20];
    
    long long dfs(int n, int last_d, int combo, vector<int>& rollMax){
        if(dp[n][last_d][combo] != -1) return dp[n][last_d][combo]; // visited before
        if(n < 0 or rollMax[last_d] < combo) return 0; // invalid
        if(n == 1) return dp[n][last_d][combo] = 1; // only roll 1 time, and last_d is set, result is 1
        long long ret = 0;
        for(int nd = 0; nd < 6; nd++){
            if(nd != last_d){
                ret = (ret + dfs(n - 1, nd, 1, rollMax)) % MOD; // combo restarts
            }
            else{
                ret = (ret + dfs(n - 1, nd, combo + 1, rollMax) % MOD); // combo continues! 
            }
        }
        return dp[n][last_d][combo] = ret % MOD;
    }
    
    int dieSimulator(int n, vector<int>& rollMax) {
        memset(dp, -1, sizeof dp);
        int ret = 0;
        for(int i = 0; i < 6; i++){
            ret = (ret + dfs(n, i, 1, rollMax)) % MOD;
        }
        return ret % MOD;
    }
};
```

## Problem Solution II [1223. Dice Roll Simulation](https://leetcode.com/problems/dice-roll-simulation/)
```python
class Solution:
    def dieSimulator(self, n: int, rollMax: List[int]) -> int:
        MOD = int(1e9 + 7)
        dp = [[0 for _ in range(10)] for _ in range(5005)] # dp[i][j] -> roll i times, ending with j
        # xy5 -> sum(dp[2]) - dp[2][5]
        # y55 -> sum(dp[1]) - dp[1][5]
        # 555 
        dp[0][6] = 1
        for i in range(1, n + 1):
            for j in range(0, 5 + 1):
                if i == 1:
                    dp[i][j] = 1
                else:
                    for k in range(0, rollMax[j]):
                        t = i - k - 1
                        if t < 0:
                            continue
                        dp[i][j] = (dp[i][j] + dp[t][6] - dp[t][j]) % MOD
                dp[i][6] = (dp[i][j] + dp[i][6]) % MOD
        return (dp[n][6]) % MOD
```
