# Leetcode_673. Number of Longest Increasing Subsequence


Use **DP LIS** to solve Leetcode_673. Number of Longest Increasing Subsequence
<!--more-->


## Problem Description [Leetcode 673](https://leetcode.com/problems/number-of-longest-increasing-subsequence/)

Given an integer array nums, return the number of longest increasing subsequences.

Notice that the sequence has to be strictly increasing.

## Examples Test Cases [Leetcode 673](https://leetcode.com/problems/number-of-longest-increasing-subsequence/)


```
Input: nums = [1,3,5,4,7]
Output: 2
Explanation: The two longest increasing subsequences are [1, 3, 4, 7] and [1, 3, 5, 7].
```


## Problem Solution [Leetcode 673](https://leetcode.com/problems/number-of-longest-increasing-subsequence/)

```cpp
class Solution {
public:
    int f[2050];
    int g[2050];
    
    int findNumberOfLIS(vector<int>& nums) {
        int ret = 0;
        int global_ret = 0;
        for(int i = 1; i <= nums.size(); i++){
            int val = nums[i - 1];
            f[i] = 1;

            // update f[i] -> just like LIS
            for(int j = 1; j <= nums.size(); j++){
                if(val > nums[j-1]){
                    f[i] = max(f[i], f[j] + 1);
                }    
            }
            ret = max(ret, f[i]);
            // update g[i] -> count of how many LIS ending with nums[i]
            for(int j = 1; j <= nums.size(); j++){
                if(f[i] == f[j] + 1 and nums[i-1] > nums[j-1]){
                    g[i] += g[j];
                }
            }
            if(g[i] == 0) g[i] = 1;
        }
        for(int i = 1; i <= nums.size(); i++){
            if(f[i] == ret){
                global_ret += g[i];    
            }
        }
        return global_ret;
    }
};
```
