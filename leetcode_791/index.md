# Leetcode_791 Custom Sort String




Use **data-structure** to solve Leetcode 791. Custom Sort String
<!--more-->

## Problem Solution [Leetcode 791. Custom Sort String](https://leetcode.com/problems/custom-sort-string/)

### Custom Comparator

```cpp
class Solution {
public:
    
    struct Node{
        char c;
        int val;

        bool operator< (const Node& w) const{
            return val < w.val;
        }   
    }node[250];
    
    int values[30];
    
    string customSortString(string order, string str) {
        
        for(int i = 0; i < order.size(); i++){
            values[order[i] - 'a'] = i + 1;
        }
        for(int i = 0; i < 30; i++){
            if(!values[i]) values[i] = order.size();
        }
        
        vector<char> ret;
        for(int i = 0; i < str.size(); i++){
            node[i] = {str[i], values[str[i] - 'a']};
        }
        sort(node, node + str.size());
        
        for(int i = 0; i < str.size(); i++){
            ret.push_back(node[i].c);
        }
        
        return string(ret.begin(), ret.end());


    }
};
```


### Count Sort

```cpp
class Solution {
public:
    int cnt[30];
    
    string customSortString(string order, string str) {
        vector<char> ret(str.size(), '.');
        for(char c : str) cnt[c - 'a'] += 1;
        int idx = 0;
        for(char c : order){
            for(int j = 0; j < cnt[c - 'a']; j++){
                ret[idx] = c;
                idx += 1;      
            }
            cnt[c - 'a'] = 0;
        }
        
        
        for(int i = 0; i < 30; i++){
            for(int j = 0; j < cnt[i]; j++)
                ret[idx++] = i + 'a';
        }
        
        return string(ret.begin(), ret.end());
        
    }
};
```
