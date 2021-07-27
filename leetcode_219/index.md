# Leetcode_219. Contains Duplicate II



## Problem Solution [Leetcode 219. Contains Duplicate II](https://leetcode.com/problems/contains-duplicate-ii/)

```cpp
class Solution {
public:
    bool containsNearbyDuplicate(vector<int>& nums, int k) {
        int n = nums.size();
        set<int> s;
        for(int i = 0; i < min(n, k + 1); i++){
            if(s.count(nums[i])) return true;
            s.insert(nums[i]);
        }
        for(int i = k + 1; i < n; i++){
            s.erase(nums[i - k - 1]);
            if(s.count(nums[i])) return true;
            s.insert(nums[i]);
        }
        return false;
    }
};
```


