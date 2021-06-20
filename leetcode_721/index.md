# Leetcode_721 Account Merge




Use **Union Find 并查集+数据结构** to solve Leetcode 721 - Account Merge
<!--more-->


```cpp
class Solution {
public:
    
    unordered_map<string, string> p;
    string find(string x){
        if(p[x] != x){
            p[x] = find(p[x]);
        }
        return p[x];
        
    }
    
    vector<vector<string>> accountsMerge(vector<vector<string>>& accounts) {
        // initialize parent
        int n = accounts.size();
        
        for(int i = 0; i < n; i++){
            for(int j = 1; j < accounts[i].size(); j++){
                p[accounts[i][j]] = accounts[i][j];
            }
        }
        
        // merge them
        for(int i = 0; i < n; i++){
            string t = find(accounts[i][1]);
            for(int j = 2; j < accounts[i].size(); j++){
                string c = find(accounts[i][j]);
                if(c != t)
                    p[c] = t;
            }
        }
        
        // root -> vector<string>
        unordered_map<string, vector<string>> temp;
        
        for(auto&& [leaf, root] : p){
            // always find root when clustering
            string t = find(root);
            if(temp.count(t)){
                temp[t].push_back(leaf);
            }
            else{
                temp[t] = {leaf};
            }
        }

        unordered_set<string> seen;
        vector<vector<string>> ret;
        
        for(int i = 0; i < n; i++){
            string name = accounts[i][0];
            vector<string> local_ret;
            
            string l = find(accounts[i][1]);
            if(!seen.count(l)){
                for(string cur : temp[l]){
                    local_ret.push_back(cur);
                }
                seen.insert(l);
            }
            if(local_ret.size() != 0)
            {
                sort(local_ret.begin(), local_ret.end());
                local_ret.insert(local_ret.begin(), name);
                ret.push_back(local_ret);
            }
        }
        return ret;   
    }
};
```
