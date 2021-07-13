# Leetcode_37  Sudoku Solver



Use **DFS** to solve Leetcode 37 - Sudoku Solver.
<!--more-->


## Problem Solution [Leetcode 37. Sudoku Solver](https://leetcode.com/problems/sudoku-solver/)

```cpp
class Solution {
public:
    
    int box[10], col[10], row[10];
    int n = 9;
    
    bool dfs(int x, int y, vector<vector<char>>& board){
        if(y == n) y = 0, x += 1;
        if(x == n){
            return true;
        }
        
        if(board[x][y] != '.') {
            return dfs(x, y + 1, board);
        }
        
        for(int i = 1; i <= 9; i++){
            if(box[x / 3 * 3 + y / 3] & (1 << i)) continue;
            if(col[x] & (1 << i)) continue;
            if(row[y] & (1 << i)) continue;
            
            box[x / 3 * 3 + y / 3] += (1 << i);
            col[x] += (1 << i);
            row[y] += (1 << i);
            board[x][y] = i + '0';
            
            if(dfs(x, y + 1, board)) return true;
            
            box[x / 3 * 3 + y / 3] -= (1 << i);
            col[x] -= (1 << i);
            row[y] -= (1 << i);
            board[x][y] = '.';
        }
        return false;
    }
    
    void solveSudoku(vector<vector<char>>& board) {
        memset(box, 0, sizeof box);
        memset(col, 0, sizeof col);
        memset(row, 0, sizeof row);
        for(int i = 0; i < n; i++){
            for(int j = 0; j < n; j++){
                if(board[i][j] == '.') continue;
                int t = board[i][j] - '0';
                box[i / 3 * 3 + j / 3] += (1 << t);
                col[i] += (1 << t);
                row[j] += (1 << t);
            }
        }
        dfs(0, 0, board);
        return;
    }
};
```


