# Leetcode_1220 Count Vowels Permutation



Use **dp** to solve Leetcode_1220 Count Vowels Permutation.
<!--more-->


## Problem Solution [1220. Count Vowels Permutation](https://leetcode.com/problems/count-vowels-permutation/)
```cpp
class Solution {
public:
    int mod = 1e9 + 7;
    long long count[5], back[5];
    int countVowelPermutation(int n) {
        for(int i = 0; i < 5; i++){
            count[i] = 1;
        }
        
        // a, e, i, o, u
        // 0, 1, 2, 3, 4
        for(int i = 1; i < n; i++){
            memcpy(back, count, sizeof count);
            count[0] = (back[1]) % mod;
            count[1] = (back[0] + back[2]) % mod;
            count[2] = (back[4] + back[3] + back[1] + back[0]) % mod;
            count[3] = (back[4] + back[2]) % mod;
            count[4] = (back[0]) % mod; 
        }    
        int ret = 0;
        for(int i = 0; i < 5; i++){
            ret = (ret + count[i]) % mod;
        }
        return ret;
    }
};
```
