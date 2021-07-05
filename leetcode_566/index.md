# Leetcode_566 Reshape the Matrix


Use **data-structure** to solve Leetcode 566 Reshape the Matrix.
<!--more-->

## Problem Solution [Leetcode_566 Reshape the Matrix](https://leetcode.com/problems/reshape-the-matrix/)

```cpp
class Solution {
public:
    vector<vector<int>> matrixReshape(vector<vector<int>>& mat, int r, int c) {
        int n = mat.size(), m = mat[0].size();
        if(n * m != r * c){
            r = n, c = m;
        }
        vector<vector<int>> ret(r, vector<int>(c, 0));
        
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                int ni = (i * m + j) / c, nj = (i * m + j) % c;
                ret[ni][nj] = mat[i][j];
            }    
        }
        return ret;
    }
};
```
