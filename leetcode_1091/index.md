# Leetcode 1091 - Shortest Path in Binary Matrix



New **BFS** to solve Leetcode 1091 - Shortest Path in Binary Matrix. 
<!--more-->



## Problem Description [Leetcode 1091](https://leetcode.com/problems/shortest-path-in-binary-matrix/)
<p>
In an N by N square grid, each cell is either empty (0) or blocked (1).

A clear path from top-left to bottom-right has length k if and only if it is composed of cells C_1, C_2, ..., C_k such that:

- Adjacent cells C_i and C_{i+1} are connected 8-directionally (ie., they are different and share an edge or corner)
- C_1 is at location (0, 0) (ie. has value grid[0][0])
- C_k is at location (N-1, N-1) (ie. has value grid[N-1][N-1])
- If C_i is located at (r, c), then grid[r][c] is empty (ie. grid[r][c] == 0).
Return the length of the shortest such clear path from top-left to bottom-right.  If such a path does not exist, return -1.

 
</p>



## Example Test Cases [Leetcode 1091](https://leetcode.com/problems/shortest-path-in-binary-matrix/)


<br>
Example1:
<br>

```
Input: [[0,1],[1,0]]
Output: 2
```


## Problem Solution [Leetcode 1091](https://leetcode.com/problems/shortest-path-in-binary-matrix/)

```cpp
// BFS
class Solution {
public:
    int shortestPathBinaryMatrix(vector<vector<int>>& grid) {
        if(grid[0][0] == 1){
            return -1;
        }
        deque<int> q;
        set<int> seen;
        int m = grid.size(), n = grid[0].size();
        int step = 1;
        seen.insert(0);
        q.push_back(0);
        while(q.size()){
            int width = q.size();
            for(int i = 0; i < width; ++i){
                int p = q.front();
                q.pop_front();
                int r = p / n, c = p % n;
                if(r == m - 1 && c == n -1){
                    return step;
                }
                for(int j = -1; j <= 1; j++){
                    for(int k = -1; k <= 1; k++){
                        if(j == 0 && k == 0){
                            continue;
                        }
                        else{
                            int nr = r + j, nc = c + k;
                            int np = nr * n + nc;
                            if(nr >= 0 && nr < m && nc >= 0 && nc < n 
                               && seen.find(np) == seen.end() && grid[nr][nc] == 0){
                                seen.insert(np);
                                q.push_back(np);
                            }
                        }
                    }
                }
            }
            step += 1;
        }
        return -1;
    }
};
```

## Problem Remark [Leetcode 1091](https://leetcode.com/problems/shortest-path-in-binary-matrix/)
- Dimension Reduction + 8 direction loop
- O(m*n) solution
