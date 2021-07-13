# Leetcode_51 N-Queens




Use **DFS** to solve Leetcode 51 - N-Queens.
<!--more-->



## Problem Solution [Leetcode 51. N-Queens](https://leetcode.com/problems/n-queens/)

```cpp
class Solution {
public:
    
    vector<vector<string>> ret;
    int n;
    int col, row, dg, udg;
    
    void dfs(int i, int j, int u, vector<vector<char>>& board){
        
        if(i == n){
            // found result
            if(u == n){
                vector<string> local_ret;
                for(auto& line : board){
                    string s(line.begin(), line.end());
                    local_ret.push_back(s);
                }
                ret.push_back(local_ret);
            }
            return;
        }
        
        // wrap up to the new row
        if(j == n) {
            dfs(i + 1, 0, u, board);
            return;
        }
        

        // not place queen
        dfs(i, j + 1, u, board);
        

        // place queen
        if(!(col & 1 << i) and !(row & 1 << j) and !(dg & 1 << (i + j)) and !(udg & 1 << (n - i + j))){
            col += 1 << i;
            row += 1 << j;
            dg += 1 << (i + j);
            udg += 1 << (n - i + j);
            board[i][j] = 'Q';
            dfs(i, j + 1, u + 1, board);
            board[i][j] = '.';
            col -= 1 << i;
            row -= 1 << j;
            dg -= 1 << (i + j);
            udg -= 1 << (n - i + j);
        }   
    }

    vector<vector<string>> solveNQueens(int target) {
        n = target;
        vector<vector<char>> board(n, vector<char>(n, '.'));
        dfs(0, 0, 0, board);
        return ret;
    }
};
```
