# Leetcode_1655 Distribute Repeating Integers


Use **DP-Bitmask** to solve Leetcode 1655 Distribute Repeating Integers.
<!--more-->


## Problem Solution [1655 - Distribute Repeating Integers](https://leetcode.com/problems/distribute-repeating-integers/)
```cpp
class Solution {
public:
    int a[55];
    int b[15];
    int f[55][(1 << 10) + 10];
    int n = 0;
    
    int dfs(int idx, int state, int m, vector<int>& quantity){
        if(state == (1 << m) - 1) return f[idx][state] = 1;
        if(idx == n) return f[idx][state] = 0;
        if(f[idx][state] != -1) return f[idx][state];
        
        int ret = 0;
        for(int n_state = 0; n_state < (1 << m); n_state += 1){
            if( (n_state & state) != state) continue; // not even cover state itself
            int sum = 0;
            for(int j = 0; j < m; j++){
                if(n_state & (1 << j)){
                    if(!(state & (1 << j))){
                        sum += quantity[j];
                    }
                }
            }
            if(sum <= a[idx]){
                ret = ret or dfs(idx + 1, n_state, m, quantity);
            }
        }
        return f[idx][state] = ret;
    }
    
    bool canDistribute(vector<int>& nums, vector<int>& quantity) {
        memset(a, 0, sizeof a);
        memset(b, 0, sizeof b);
        memset(f, -1, sizeof f);
        unordered_map<int, int> mp;
        for(int num : nums) {
            if(mp.count(num)) mp[num] += 1;
            else mp[num] = 1;
        }
        for(auto p : mp) a[n++] = p.second;
        int m = quantity.size();
        return dfs(0, 0, m, quantity);

    }
};
```
