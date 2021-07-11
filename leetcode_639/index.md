# Leetcode_639 Decode Ways II




Use **dp** to solve Leetcode_639 Decode Ways II
<!--more-->


## Problem Description [Leetcode 639](https://leetcode.com/problems/decode-ways-ii/)

<p>
A message containing letters from A-Z can be encoded into numbers using the following mapping:

```
'A' -> "1"
'B' -> "2"
...
'Z' -> "26"
```

To decode an encoded message, all the digits must be grouped then mapped back into letters using the reverse of the mapping above (there may be multiple ways). For example, "11106" can be mapped into:

```
"AAJF" with the grouping (1 1 10 6)
"KJF" with the grouping (11 10 6)
```

Note that the grouping (1 11 06) is invalid because "06" cannot be mapped into 'F' since "6" is different from "06".

In addition to the mapping above, an encoded message may contain the '*' character, which can represent any digit from '1' to '9' ('0' is excluded). For example, the encoded message "1*" may represent any of the encoded messages "11", "12", "13", "14", "15", "16", "17", "18", or "19". Decoding "1*" is equivalent to decoding any of the encoded messages it can represent.

Given a string s containing digits and the '*' character, return the number of ways to decode it.

Since the answer may be very large, return it modulo 109 + 7.
</p>


## Example Test Cases [Leetcode 639](https://leetcode.com/problems/decode-ways-ii/)

```
Input: s = "*"
Output: 9
Explanation: The encoded message can represent any of the encoded messages "1", "2", "3", "4", "5", "6", "7", "8", or "9".
Each of these can be decoded to the strings "A", "B", "C", "D", "E", "F", "G", "H", and "I" respectively.
Hence, there are a total of 9 ways to decode "*".
```


```
Input: s = "1*"
Output: 18
Explanation: The encoded message can represent any of the encoded messages "11", "12", "13", "14", "15", "16", "17", "18", or "19".
Each of these encoded messages have 2 ways to be decoded (e.g. "11" can be decoded to "AA" or "K").
Hence, there are a total of 9 * 2 = 18 ways to decode "1*".
```


## Problem Solution [Leetcode 639](https://leetcode.com/problems/decode-ways-ii/)



```cpp
class Solution {
public:
    static const int MOD = 1E9 + 7;
    
    
    // dp[i][0] -> ending with none, 3, 4, 5, 6, 7, 8, 9 = dp[i-1][1] * 10 | 9 + dp[i-1][2] * 7 | 6 + dp[i][0] * 9
    // dp[i][1] -> single 1 = dp[i-1][0] 
    // dp[i][2] -> single 2 = dp[i-1][0] 
    // dp[i][3] -> ending with 3, 4, 5, 6, 7, 8, 9 = dp[i-1][]
    
    
    static const int N = 1e5 + 10;
    
    long long dp[N][27];
    
    int numDecodings(string s) {
        memset(dp, 0, sizeof dp);
        int n = s.size();
        dp[0][0] = 1;
        for(int i = 1; i <= s.size(); i++){
            char c = s[i-1];
            if(c == '*'){
                dp[i][0] = (dp[i-1][1] * 9 + dp[i-1][2] * 6 + dp[i-1][0] * 9) % MOD;
                dp[i][1] = (dp[i-1][0]) % MOD;
                dp[i][2] = (dp[i-1][0]) % MOD;
            }
            else{
                int t = c - '0';
                if(t == 0){
                    dp[i][0] = (dp[i-1][1] + dp[i-1][2]) % MOD;
                }
                else if(t == 1){
                    dp[i][0] = (dp[i-1][1] + dp[i-1][2] + dp[i-1][0]) % MOD;
                    dp[i][1] = (dp[i-1][0]) % MOD;
                }
                else if(t == 2){
                    dp[i][0] = (dp[i-1][1] + dp[i-1][2] + dp[i-1][0]) % MOD;
                    dp[i][2] = (dp[i-1][0]) % MOD;
                }
                else if(t <= 6){
                    dp[i][0] = (dp[i-1][1] + dp[i-1][2] + dp[i-1][0]) % MOD;
                }
                else if(t <= 9){
                    dp[i][0] = (dp[i-1][1] + dp[i-1][0]) % MOD;
                }
            }
        }

        return (dp[n][0]) % MOD;
    }  
};
```
