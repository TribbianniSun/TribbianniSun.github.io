# Leetcode 1010 Pairs of Songs With Total Durations Divisible by 60




Use **data-structure** to solve Leetcode 1010. Pairs of Songs With Total Durations Divisible by 60
<!--more-->

## Problem Solution [Leetcode 1010. Pairs of Songs With Total Durations Divisible by 60](https://leetcode.com/problems/pairs-of-songs-with-total-durations-divisible-by-60/)

```cpp
class Solution {
public:
    
    int freq[65];
    
    int numPairsDivisibleBy60(vector<int>& time) {
        int ret = 0;
        memset(freq, 0, sizeof freq);

        for(int num : time){
            int remain = num % 60;
            int target = (60 - remain) % 60;
            ret += freq[target];
            freq[remain] += 1;
        }
        
        return ret;
        
    }
    
};
```
