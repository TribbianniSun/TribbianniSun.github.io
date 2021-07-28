# Leetcode_1493 Longest Subarray of 1's After Deleting One Element


Use **sliding-window** to solve Leetcode_1493 Longest Subarray of 1's After Deleting One Element
<!--more-->


## Problem Solution [Leetcode 1493 Longest Subarray of 1's After Deleting One Element](https://leetcode.com/problems/longest-subarray-of-1s-after-deleting-one-element/)


```CPP
class Solution {
public:
    int longestSubarray(vector<int>& nums) {
        int s = 0, n = nums.size();
        for(int num : nums) s += num;
        if(s == n) return s - 1;
        
        
        int counter = 0;
        int ret = 0;
        for(int i = 0, j = 0; i < n; i++){
            
            // added nums[i] to the sliding window
            if(nums[i] == 0) counter += 1;
            
            // while loop to make sure that the sliding window is valid
            while(j <= i and counter > 1){
                if(nums[j] == 0){
                    counter -= 1;
                }
                j += 1;
            }
            
            // update the result
            ret = max(ret, i - j + 1 - counter);
        }
        
        
        return ret;

    }
};
```
