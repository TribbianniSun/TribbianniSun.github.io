# Leetcode_1931 Painting a Grid With Three Different Colors


Use **dp, bitmask, dfs** to solve Leetcode_1931 Painting a Grid With Three Different Colors
<!--more-->

## Problem Description [Leetcode_1931 Painting a Grid With Three Different Colors](https://leetcode.com/problems/painting-a-grid-with-three-different-colors/)

<p>
You are given two integers m and n. Consider an m x n grid where each cell is initially white. You can paint each cell red, green, or blue. All cells must be painted.

Return the number of ways to color the grid with no two adjacent cells having the same color. Since the answer can be very large, return it modulo 109 + 7.

</p>



## Example Test Cases [Leetcode_1931 Painting a Grid With Three Different Colors](https://leetcode.com/problems/painting-a-grid-with-three-different-colors/)


```
Input: m = 1, n = 2
Output: 6
Explanation: The six possible colorings are shown in the image above.
```



## Problem Solution [Leetcode_1931 Painting a Grid With Three Different Colors](https://leetcode.com/problems/painting-a-grid-with-three-different-colors/)

```cpp
class Solution {
public:
    static const int MOD = 1e9 + 7;
    int idx = 0;
    int target;
    
    vector<int> ways[1005];
    
    vector<int> graph[1005];
    
    int path[10];
    
    int dp[1005][1005];
    
    inline void dfs(int u){
        if(u == target){
            for(int i = 0; i < target; i++){
                ways[idx].push_back(path[i]);
            }
            idx += 1;
            return;
        }
        
        for(int i = 1; i <= 3; i+=1){
            if(u == 0 or path[u-1] != i){
                path[u] = i;
                dfs(u + 1);
                path[u] = 0;
            }
        }
    }
    
    bool check(vector<int>& p, vector<int>& q){
        for(int i = 0; i < target; i++){
            if(p[i] == q[i]) return false;
        }
        return true;
    }
    
    int colorTheGrid(int m, int n) {
        target = m;
        dfs(0);
        for(int i = 0; i < idx; i++){
            for(int j = 0; j < idx; j++){
                if(check(ways[i], ways[j]))
                    graph[i].push_back(j);
            }
        }
        
        vector<vector<int>> dp(n + 1, vector<int>(idx + 1, 0));
        for(int i = 0; i < idx; i++) dp[0][i] = 1;
        
        for(int i = 0; i < n; i++){
            for(int j = 0; j < idx; j++){
                // before we are at j
                for(int k : graph[j]){
                    dp[i + 1][k] = (dp[i + 1][k] + dp[i][j]) % MOD;
                }
            }
        }
        
        int ret = 0;
        for(int i = 0; i < idx; i++){
            ret = (ret + dp[n-1][i]) % MOD;
        }
        
        return ret;
        
        
    }
};
```
