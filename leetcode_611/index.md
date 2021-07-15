# Leetcode_611 Valid Triangle Number



Use **binary-index-tree, two-pointer** to solve Leetcode_611 Valid Triangle Number
<!--more-->


## Problem Solution [Leetcode 611. Valid Triangle Number](https://leetcode.com/problems/valid-triangle-number/)




### two-pointer

```cpp
class Solution {
public:
    int triangleNumber(vector<int>& nums) {
        sort(nums.begin(), nums.end());
                
        int ret = 0;
        for(int k = nums.size() - 1; k > 1; k--){
            for(int i = 0, j = k - 1; j > i; ){
                if(nums[i] + nums[j] > nums[k]){
                    ret += (j - i);
                    j -= 1;
                }
                else{
                    i += 1;
                }
            }
            cout << ret;
        }
        return ret;
    }
};
```



### binary-index-tree

```cpp
class Solution {
public:
    
    static const int N = 1003;
    
    int freq[1005];
    
    int lowbit(int t){
        return t & -t;
    }
    
    void update(int c, int x){
        for(int i = c; i < N; i += lowbit(i)){
            freq[i] += x;
        }
    }
    
    int query(int u){
        int ret = 0;
        for(int i = u; i; i -= lowbit(i)){
            ret += freq[i];
        }
        return ret;
    }
    
    
    int triangleNumber(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        memset(freq, 0, sizeof freq);
        int n = nums.size();
        
        for(int num : nums){
            if(num == 0) continue;
            update(num, 1);
        }    
        
        int ret = 0;
        
        for(int i = 0; i < n; i++){
            if(nums[i] == 0) continue;
            update(nums[i], -1);
            for(int j = i + 1; j < n; j++){
                if(nums[j] == 0) continue;
                
                update(nums[j], -1);
                
                int r = min(nums[i] + nums[j] - 1, 1001);
                int l = abs(nums[i] - nums[j]) + 1;
                
                if(l > r) continue;
                
                ret += (query(r) - query(l - 1));
                
            }
            for(int j = i + 1; j < n; j++) update(nums[j], 1);
        }
        
        return ret;
    }
};
```




