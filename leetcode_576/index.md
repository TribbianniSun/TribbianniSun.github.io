# Leetcode_576



Use **Dynamic Programmingn** to solve Leetcode 576 - Out of Boundary Paths.
<!--more-->

## Problem Solution [Leetcode 576](https://leetcode.com/problems/out-of-boundary-paths/)

```cpp
class Solution {
public:
    int dx[4] = {-1, 0, 1, 0};
    int dy[4] = {0, 1, 0, -1};
    
    int cur_f[55][55];
    int next_f[55][55];
    
    int MOD = 1e9 + 7;
    
    int findPaths(int m, int n, int maxMove, int sr, int sc) {
        long long count = 0;
        cur_f[sr][sc] = 1;
        for(int t = 0; t < maxMove; t++){
            memset(next_f, 0, sizeof next_f);
            for(int i = 0; i < m; i++){
                for(int j = 0; j < n; j++){
                    for(int k = 0; k < 4; k++){
                        int ni = i + dx[k], nj = j + dy[k];
                        if(ni < 0 or ni >= m or nj < 0 or nj >= n) count = (count + cur_f[i][j]) % MOD;
                        else next_f[ni][nj] = (next_f[ni][nj] + cur_f[i][j]) % MOD;
                    }
                }
            }
            memcpy(cur_f, next_f, sizeof next_f);
        }
        return count;
    }
};
```
