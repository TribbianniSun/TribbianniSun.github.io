# Leetcode_363 Max Sum of Rectangle No Larger Than K



New **data-structure** to solve Leetcode 89 - Gray Code.
<!--more-->


## Problem Description [leetcode 363](https://leetcode.com/problems/max-sum-of-rectangle-no-larger-than-k/)
<p>
Given an m x n matrix matrix and an integer k, return the max sum of a rectangle in the matrix such that its sum is no larger than k.

It is guaranteed that there will be a rectangle with a sum no larger than k.
</p>



## Example Test Cases [leetcode 363](https://leetcode.com/problems/max-sum-of-rectangle-no-larger-than-k/)

```
Input: matrix = [[1,0,1],[0,-2,3]], k = 2
Output: 2
Explanation: Because the sum of the blue rectangle [[0, 1], [-2, 3]] is 2, and 2 is the max number no larger than k (k = 2).
```




## Problem Solution [leetcode 363](https://leetcode.com/problems/max-sum-of-rectangle-no-larger-than-k/)

```cpp
// step1: prefix sum in column

// step2: pick two row, i, j, the sum inside;  

// step3, assume current culmative sum is s, s - x <= k => s - k <= x, we need to find something that must be bigger than or equal to s - k, then we got x, set(red black tree)


// 1  0   1
// 1  -2  4


class Solution {
public:
    int f[105][105];
    int maxSumSubmatrix(vector<vector<int>>& matrix, int k) {
        memset(f, 0, sizeof f);
        
        // step1
        int n = matrix.size(), m = matrix[0].size();
        for(int j = 1; j <= m; j++){
            for(int i = 1; i <= n; i++){
                int val = matrix[i-1][j-1];
                f[i][j] = f[i-1][j] + val;
            }
        }

        int ret = -2e9;
        // step2
        for(int i = 1; i <= n; i++){
            for(int j = i; j <= n; j++){
                set<int> s;
                s.insert(0);
                int sum = 0;
                for(int kk = 1; kk <= m; kk++){
                    int val = f[j][kk] - f[i-1][kk];
                    sum += val;
                    int x = sum - k;
                    auto it = s.lower_bound(x);

                    if(it == s.end()){
                        s.insert(sum);
                        continue;
                    } 
                    else{
                        int cur = sum - (*it);
                        ret = max(ret, cur);
                        s.insert(sum);
                    }
                }
                cout << endl;
            }
        }
        return ret;
    }
};
```




