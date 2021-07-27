# Leetcode_643 Maximum Average Subarray I



## Problem Solution [Leetcode 643. Maximum Average Subarray I](https://leetcode.com/problems/maximum-average-subarray-i/)

```cpp
class Solution {
public:
    double findMaxAverage(vector<int>& nums, int k) {
        int n = nums.size();
        double cur = 0;
        double max_sum = -2e9;
        for(int i = 0; i < k; i++){
            cur += nums[i];
        }
        for(int i = k; i < n; i++){
            max_sum = max(max_sum, cur);
            cur -= nums[i - k];
            cur += nums[i];
        }
        max_sum = max(max_sum, cur);
        
        return max_sum / k;
    }
};
```
