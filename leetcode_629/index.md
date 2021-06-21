# Leetcode_629 K Inverse Pairs Array


Use **Dynamic Programming + Prefix Sum** to solve Leetcode 629 - K Inverse Pairs Array
<!--more-->


## Problem Description [Leetcode 629](https://leetcode.com/problems/k-inverse-pairs-array/)


<p>
For an integer array nums, an inverse pair is a pair of integers [i, j] where 0 <= i < j < nums.length and nums[i] > nums[j].

Given two integers n and k, return the number of different arrays consist of numbers from 1 to n such that there are exactly k inverse pairs. Since the answer can be huge, return it modulo 109 + 7.
</p>


## Example Test Cases [Leetcode 629](https://leetcode.com/problems/k-inverse-pairs-array/)

```
Input: n = 3, k = 0
Output: 1
Explanation: Only the array [1,2,3] which consists of numbers from 1 to 3 has exactly 0 inverse pairs.
```


## Problem Solution [Leetcode 629](https://leetcode.com/problems/k-inverse-pairs-array/)

```cpp
class Solution {
public:
    
    // n, 0 -> 1
    
    // f(n, k) -> n, k 
    // n, 0 -> (n - 1, 0) -> 1
    // n, 1 -> (n - 1, 1) + (n - 1, 0) 
    // n, 2 -> (n - 1, 2) + (n - 1, 1) + (n - 1, 0) -> (n, 1) + (n - 1, 2)
    
    
    
    // f(n, m) = f(n - 1, 0) + f(n - 1, 1) + .... f(n - 1, m - 1), + f(n - 1, m)
    // f(n, m) = not always like that if m >= n, then f(n, m) = f(n-1, m-n+1) + f(n-1, m-n+2) ... + f(n, m)
    // prefix sum + dp
    
    unsigned int f[1005][1005];
    unsigned int s[1005][1005];
    int MOD = 1e9 + 7;
    int kInversePairs(int n, int k) {
        
        memset(f, 0, sizeof f);
        
        for(int i = 0; i <= n; i++){
            f[i][0] = 1;
            s[i][0] = 1;
        }
        
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= min(i * (i - 1) / 2, k); j++){
                if(j >= i) f[i][j] = (s[i-1][j] - s[i-1][j-i] + MOD) % MOD; // f(3, 3) -> f(2, 1) + f(2, 0)
                                                                            // f(n, m) where n >= m -> f(n-1, m-n+1) + f(n-1, m-n+2) ... + f(n, m)
                else f[i][j] = s[i-1][j];
            }
            for(int j = 1; j <= min(i*i+i, k); j++){
                s[i][j] = (s[i][j-1] + f[i][j] + MOD) % MOD;
            }
        }
        return f[n][k];
    }
};

```
