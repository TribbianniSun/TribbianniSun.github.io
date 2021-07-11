# Leetcode_1930 Unique Length-3 Palindromic Subsequences



Use **array** to solve Leetcode_1930 Unique Length-3 Palindromic Subsequences
<!--more-->


## Problem Solution [Leetcode_1930 Unique Length-3 Palindromic Subsequences](https://leetcode.com/problems/unique-length-3-palindromic-subsequences/)


```cpp
class Solution {
public:
    int freq[30];
    
    int countPalindromicSubsequence(string s) {
        int n = s.size();
        int ret = 0;
        for(int i = 0; i < 26; i++){
            char c = i + 'a';
            int l = 0, r = n - 1;
            while(l < n){
                if(s[l] == c) break;
                else l += 1;
            }
            while(r >= 0){
                if(s[r] == c) break;
                else r -= 1;
            }
            memset(freq, 0, sizeof freq);
            for(int k = l + 1; k < r; k++){
                if(freq[s[k] - 'a'] == 0) ret += 1; 
                freq[s[k] - 'a'] += 1;
            }
        }
        
        return ret;
    }
};
```

