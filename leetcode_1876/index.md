# Leetcode_1876 Substrings of Size Three with Distinct Characters


Use **sliding-window** to solve Leetcode_1876 Substrings of Size Three with Distinct Characters
<!--more-->

## Problem Solution [Leetcode 1876. Substrings of Size Three with Distinct Characters](https://leetcode.com/problems/substrings-of-size-three-with-distinct-characters/)

```cpp
class Solution {
public:
    int countGoodSubstrings(string s) {
        int n = s.size();
        if(n < 3) return 0;
        int freq[30];
        memset(freq, 0, sizeof freq);
        int counter = 0;
        int ret = 0;
        for(int i = 0; i < 3; i+=1){
            if(!freq[s[i] - 'a']++) counter += 1;
        }
        for(int i = 3; i < n; i++){
            if(counter == 3) ret += 1;
            freq[s[i-3]-'a'] -= 1;
            if(freq[s[i-3]-'a'] == 0){
                counter -= 1;
            }
            if(!freq[s[i] - 'a']++) counter += 1;
        }
        if(counter == 3) ret += 1;
        return ret;
    }
};
```

