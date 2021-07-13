# Leetcode_52 - N-Queens II



Use **DFS** to solve Leetcode 52 - N-Queens II.
<!--more-->


## Problem Solution [Leetcode 52. N-Queens II](https://leetcode.com/problems/n-queens-ii/submissions/)


```cpp
class Solution {
public:
    int ret, n, col, row, dg, udg;
    
    void dfs(int i, int j, int u){
        
        if(j == n){
            dfs(i + 1, 0, u);
            return;
        }
        
        if(i == n){
            if(u == n)
            {
                ret += 1;
            }
            return;
        }
        
        dfs(i, j + 1, u);
        
        if(!(col & 1 << i) and !(row & 1 << j) and !(dg & 1 << (i + j)) and !(udg & 1 << (n - 1 - i + j))){
            col += 1 << i;
            row += 1 << j;
            dg += 1 << (i + j);
            udg += 1 << (n - 1 - i + j);
            dfs(i, j + 1, u + 1);
            col -= 1 << i;
            row -= 1 << j;
            dg -= 1 << (i + j);
            udg -= 1 << (n - 1 - i + j);
        }   
                
    }
    
    int totalNQueens(int target) {
        
        ret = 0, n = target, col = 0, row = 0, dg = 0, udg = 0;
        dfs(0, 0, 0);      
        return ret;
        
    }
};
```


