# Leetcode_730 Count Different Palindromic Subsequences



Use **DP** to solve Leetcode 730 - Count Different Palindromic Subsequences.
<!--more-->

## Problem Description [Leetcode 730 - Count Different Palindromic Subsequences](https://leetcode.com/problems/count-different-palindromic-subsequences/)


<p>
Given a string s, return the number of different non-empty palindromic subsequences in s. Since the answer may be very large, return it modulo 109 + 7.

A subsequence of a string is obtained by deleting zero or more characters from the string.

A sequence is palindromic if it is equal to the sequence reversed.

Two sequences a1, a2, ... and b1, b2, ... are different if there is some i for which ai != bi.
</p>


## Example Test Cases [Leetcode 730 - Count Different Palindromic Subsequences](https://leetcode.com/problems/count-different-palindromic-subsequences/)

```
Input: s = "bccb"
Output: 6
Explanation: The 6 different non-empty palindromic subsequences are 'b', 'c', 'bb', 'cc', 'bcb', 'bccb'.
Note that 'bcb' is counted only once, even though it occurs twice.
```

## Problem Solution [Leetcode 730 - Count Different Palindromic Subsequences](https://leetcode.com/problems/count-different-palindromic-subsequences/)
```cpp
class Solution {
public:
    int MOD = 1e9 + 7;
    int f[1005][1005][5];
    
    int dp(int l, int r, char c, string& s){
        // dp[l][r][c] -> [l, r] bounded by c
        if(f[l][r][c-'a'] != -1) return f[l][r][c-'a'];
        if(l > r) return f[l][r][c-'a'] = 0;
        else if(l == r){
            if(s[l] == c){
                return f[l][r][c-'a'] = 1;
            }
            else{
                return f[l][r][c-'a'] = 0;
            }
        }
        else if(s[l] == s[r] and s[l] == c){
            int ret = 0;
            for(int i = 0; i < 4; i++){
                ret = (ret + dp(l + 1, r - 1, i + 'a', s)) % MOD;
            }
            return f[l][r][c-'a'] = (2 + ret) % MOD;
        }
        else{
            int ret = 0;
            ret = (ret + dp(l + 1, r, c, s)) % MOD;
            ret = (ret + dp(l, r - 1, c, s)) % MOD;
            ret = (ret - dp(l + 1, r - 1, c, s) + MOD) % MOD;
            return f[l][r][c-'a'] = ret % MOD;
        }
        return -1;
    }
    
    int countPalindromicSubsequences(string s) {
        memset(f, -1, sizeof f);
        int ret = 0;
        for(int i = 0; i < 4; i++){
            ret = (ret + dp(0, s.size() - 1 , i + 'a', s)) % MOD;
        }
        return ret;
    }
};
```

## Problem Analysis

bounded by last character, add one more dimension

### l > r
- 0

### l = r,
- check if s[l] == c?

### s[l] == s[r] and s[l] == c
- ret + dp(l + 1, r - 1, 0 + 'a', s)
- ret + dp(l + 1, r - 1, 1 + 'a', s)
- ret + dp(l + 1, r - 1, 2 + 'a', s)
- ret + dp(l + 1, r - 1, 3 + 'a', s)


### otherwise, 
- ret = (ret + dp(l + 1, r, c, s)) % MOD;
- ret = (ret + dp(l, r - 1, c, s)) % MOD;
- ret = (ret - dp(l + 1, r - 1, c, s) + MOD) % MOD;
