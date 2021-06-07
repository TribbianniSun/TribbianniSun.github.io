# Leetcode_934 - Shortest Bridge




Use **BFS 最短路模型** to solve Leetcode 934 - Shortest Bridge
<!--more-->



## Problem Description [Leetcode 934](https://leetcode.com/problems/shortest-bridge/)


<p>

In a given 2D binary array grid, there are two islands.  (An island is a 4-directionally connected group of 1s not connected to any other 1s.)

Now, we may change 0s to 1s so as to connect the two islands together to form 1 island.

Return the smallest number of 0s that must be flipped.  (It is guaranteed that the answer is at least 1.)

</p>



## Example Test Cases [Leetcode 934](https://leetcode.com/problems/shortest-bridge/)


```
Input: grid = [[1,1,1,1,1],[1,0,0,0,1],[1,0,1,0,1],[1,0,0,0,1],[1,1,1,1,1]]
Output: 1
```

## Problem Solution [Leetcode 934](https://leetcode.com/problems/shortest-bridge/)

```cpp
typedef pair<int, int> PII;

class Solution {
public:
    int st[150][150]; // 0 -> not explored in finding first island, 1 -> in the first island, 3 -> not explored in expanding process
    
    int n, m;
    int dx[4] = {-1, 0, 1, 0}, dy[4] = {0, 1, 0, -1};
    
    void bfs_first_island(int sx, int sy, vector<vector<int>>& grid){
        queue<PII> q;
        q.push({sx, sy});
        st[sx][sy] = 1;
        while(q.size()){
            PII it = q.front(); q.pop();
            int i = it.first, j = it.second;
            for(int k = 0; k < 4; k++){
                int ni = i + dx[k], nj = j + dy[k];
                if(ni < 0 or ni >= n or nj < 0 or nj >= m) continue;
                if(st[ni][nj] != 0) continue;
                if(grid[ni][nj] != 1) continue;
                st[ni][nj] = 1;
                q.push({ni, nj});
            }
        }
    }
    
    
    int bfs_connect(vector<vector<int>>& grid){
        queue<PII> q;
        
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(st[i][j] == 1)
                {
                    st[i][j] = 3;
                    cout << i << " " << j << endl;
                    q.push({i, j});                    
                }
            }
        }
        
        int step = 0;
        while(q.size()){
            int s = q.size();
            step += 1;
            for(int i = 0; i < s; i++){
                PII it = q.front(); q.pop();
                int x = it.first, y = it.second;
                for(int k = 0; k < 4; k++){
                    int nx = x + dx[k], ny = y + dy[k];
                    if(nx < 0 or nx >= n or ny < 0 or ny >= m) continue;
                    if(st[nx][ny] == 3) continue;
                    q.push({nx, ny});
                    st[nx][ny] = 3;
                    if(grid[nx][ny] == 1) return step;
                }
            }
        }
        return step;
    }
    
    int shortestBridge(vector<vector<int>>& grid) {
        n = grid.size(), m = grid[0].size();
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(grid[i][j] == 1){
                    bfs_first_island(i, j, grid);
                    return bfs_connect(grid) - 1;
                }
            }
        }    

        return -1;        
    }
};

// 0,1,0,0,0
// 0,1,0,1,1
// 0,0,0,0,1
// 0,0,0,0,0
// 0,0,0,0,0
```


