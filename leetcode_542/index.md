# Leetcode_542 01 Matrix



## Problem Description [Leetcode 542](https://leetcode.com/problems/01-matrix/)
<p>

Given an m x n binary matrix mat, return the distance of the nearest 0 for each cell.

The distance between two adjacent cells is 1.

</p>


## Example Test Cases [Leetcode 542](https://leetcode.com/problems/01-matrix/)



![test case 1](https://assets.leetcode.com/uploads/2021/04/24/01-1-grid.jpg)
```
Input: mat = [[0,0,0],[0,1,0],[0,0,0]]
Output: [[0,0,0],[0,1,0],[0,0,0]]
```



## Problem Solution [Leetcode 542](https://leetcode.com/problems/01-matrix/)

```cpp
typedef pair<int,int> PII;

class Solution {
public:
    int n, m;
    int dx[4] = {0, 0, -1, 1};
    int dy[4] = {1, -1, 0, 0};
    
    vector<vector<int>> updateMatrix(vector<vector<int>>& mat) {
        n = mat.size(), m = mat[0].size();
        vector<vector<bool>> st(n, vector<bool>(m, false));
        vector<vector<int>> ret(n, vector<int>(m, 0));
        queue<PII> q;
        
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(mat[i][j] == 0){
                    ret[i][j] = 0;
                    st[i][j] = true;
                    q.push({i, j});
                }
            }
        }
        
        while(q.size()){
            PII c = q.front(); q.pop();
            int i = c.first, j = c.second;
            for(int k = 0; k < 4; k++){
                int ni = dx[k] + i, nj = dy[k] + j;
                if(ni < 0 or ni >= n or nj < 0 or nj >= m) continue;
                if(st[ni][nj]) continue;
                ret[ni][nj] = ret[i][j] + 1;
                st[ni][nj] = true;
                q.push({ni, nj});
            }
        }
        return ret;
    }
};
```

## Problem Remark [Leetcode 542](https://leetcode.com/problems/01-matrix/)
- classic multiple source BFS
- similar to [Leetcode 934](https://leetcode.com/problems/shortest-bridge/)
