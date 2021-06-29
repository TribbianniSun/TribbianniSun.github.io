# Leetcode_1004 Max Consecutive Ones III



Use **two-pointer, binary-search** to solve Leetcode_1004 Max Consecutive Ones III.
<!--more-->


## Problem Description [Leetcode 1004 Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/)

<p>
Given a binary array nums and an integer k, return the maximum number of consecutive 1's in the array if you can flip at most k 0's.
</p>



## Test Cases [Leetcode 1004 Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/)

```
Input: nums = [1,1,1,0,0,0,1,1,1,1,0], k = 2
Output: 6
Explanation: [1,1,1,0,0,1,1,1,1,1,1]
Bolded numbers were flipped from 0 to 1. The longest subarray is underlined.
```

## Problem Solution [Leetcode 1004 Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/)

```cpp
class Solution {
public:
    
    bool check(int len, vector<int>& prefix_sum, int n, int k){
        for(int start = 1, end = start + len - 1; end <= n; start++, end++){
            int count = prefix_sum[end] - prefix_sum[start - 1];
            if(count + k >= len) return true;
        }    
        return false;
    }
    
    int longestOnes_Binary_Search(vector<int>& nums, int k) {
        int n = nums.size();
        vector<int> prefix_sum(n + 5, 0);
        for(int i = 1; i <= n; i++){
            prefix_sum[i] = prefix_sum[i-1] + nums[i - 1];
        }
        int l = 0, r = n;
        while(l < r){
            int mid = (l + r + 1) / 2;
            if(check(mid, prefix_sum, n, k)) l = mid;
            else r = mid - 1;
        }
        return l;
    }
    
    
    int longestOnes_Sliding_Window(vector<int>& nums, int k) {
        int n = nums.size();
        vector<int> prefix_sum(n + 5, 0);
        for(int i = 1; i <= n; i++){
            prefix_sum[i] = prefix_sum[i-1] + nums[i - 1];
        }
       
        int ret = 0;
        
        for(int i = 1, j = 1; i <= n; i++){
            while(j <= n and prefix_sum[j] - prefix_sum[i-1] + k >= j - i + 1){
                ret = max(ret, j - i + 1);
                j += 1;
            }
        }
        
        return ret;
    }
    
    int longestOnes(vector<int>& nums, int k) {
        
    }  
};
