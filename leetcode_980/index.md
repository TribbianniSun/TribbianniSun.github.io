# Leetcode_980 Unique Paths III



Use **dfs** to solve Leetcode_980 Unique Paths III
<!--more-->


## Problem Solution [Leetcode 980. Unique Paths III](https://leetcode.com/problems/unique-paths-iii/)

```cpp
class Solution {
public:
    int ret = 0;
    int m, n, target;
    
    int si, sj;
    
    int dx[4] = {0, 0, -1, 1};
    int dy[4] = {1, -1, 0, 0};
    
    inline void dfs(int i, int j, int count, vector<vector<int>> grid){
        if(grid[i][j] == 2){
            ret += (target == count);
            return;
        }
        
        for(int k = 0; k < 4; k++){
            int ni = i + dx[k], nj = j + dy[k];
            if(ni < 0 or ni >= n or nj < 0 or nj >= m) continue;
            if(grid[ni][nj] != 2 and grid[ni][nj] != 0) continue;
            if(grid[ni][nj] == 0){
                grid[ni][nj] = 5;
                dfs(ni, nj, count + 1, grid);
                grid[ni][nj] = 0;
            }
            else{
                dfs(ni, nj, count, grid);
            }
        }
    }
    
    int uniquePathsIII(vector<vector<int>>& grid) {
        n = grid.size(), m = grid[0].size();
        
        for(int i = 0; i < n; i++)
            for(int j = 0; j < m; j++)
            {
                if(grid[i][j] == 0)
                    target += 1;
                else if(grid[i][j] == 1){
                    si = i, sj = j;
                }
            }
                
        dfs(si, sj, 0, grid);
        return ret;
    }
};
```

