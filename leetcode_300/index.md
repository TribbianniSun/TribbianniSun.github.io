# Leetcode_300 Longest Increasing Subsequence


Use **DP LIS** to solve Leetcode_300 Longest Increasing Subsequence.
<!--more-->

## Problem Description [Leetcode 300](https://leetcode.com/problems/longest-increasing-subsequence/)

Given an integer array nums, return the length of the longest strictly increasing subsequence.

A subsequence is a sequence that can be derived from an array by deleting some or no elements without changing the order of the remaining elements. For example, [3,6,2,7] is a subsequence of the array [0,3,1,6,2,2,7].

## Examples Test Cases [Leetcode 300](https://leetcode.com/problems/longest-increasing-subsequence/)

```
Input: nums = [10,9,2,5,3,7,101,18]
Output: 4
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.
```

## Problem Solution [Leetcode 300](https://leetcode.com/problems/longest-increasing-subsequence/)


```cpp
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        set<int> tails;
        for(int num : nums){
            auto it = tails.lower_bound(num);
            if(it != tails.end()){
                tails.erase(it);
            }
            tails.insert(num);
        }
        return tails.size();
    }
};
```
