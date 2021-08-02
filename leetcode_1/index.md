# Leetcode_1 Two Sum


Use **data-structure** to solve Leetcode 1 Two Sum.
<!--more-->

## Problem Solution [Leetcode 1. Two Sum](https://leetcode.com/problems/two-sum/)

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> mp;
        for(int i = 0; i < nums.size(); i++){
            mp[target - nums[i]] = i;
        }
        for(int i = 0; i < nums.size(); i++){
            if(mp.count(nums[i]) and mp[nums[i]] != i) return {i, mp[nums[i]]};
        }
        return {};
    }
};
```
