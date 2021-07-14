# Leetcode_205 Isomorphic Strings



Use **data-structure** to solve Leetcode_162 Find Peak Element.
<!--more-->


## Problem Solution [Leetcode 205. Isomorphic Strings](https://leetcode.com/problems/isomorphic-strings/)
```cpp
class Solution {
public:
    
    int s_t[300], t_s[300];
    
    bool isIsomorphic(string s, string t) {
        memset(s_t, -1, sizeof s_t);
        memset(t_s, -1, sizeof t_s);
        
        for(int i = 0; i < s.size(); i++){
            int sidx = s[i], tidx = t[i];
            if(s_t[sidx] == -1)
                s_t[sidx] = tidx;
            else
                if(s_t[sidx] != tidx) return false;
            
            if(t_s[tidx] == -1)
                t_s[tidx] = sidx;
            else
                if(t_s[tidx] != sidx) return false;
        }
        
        return true;
    }
};
```
