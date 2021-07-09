# Leetcode_300_II Longest Increasing Subsequence



Use **DP** to solve Leetcode_300 Longest Increasing Subsequence.
<!--more-->

## Problem Solution [Leetcode 300 Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)

```cpp
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        set<int> s;
        for(int num : nums){
            auto it = s.lower_bound(num);
            if(it != s.end()) s.erase(it);
            s.insert(num);
        }
        return s.size();
    }
};
```


