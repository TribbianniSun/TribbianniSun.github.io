# Leetcode_990 Satisfiability of Equality Equations




Use **union-find 裸并查集** to solve Leetcode 990 - Satisfiability of Equality Equations
<!--more-->



## Problem Description [Leetcode 990](https://leetcode.com/problems/satisfiability-of-equality-equations/)


<p>
Given an array equations of strings that represent relationships between variables, each string equations[i] has length 4 and takes one of two different forms: "a==b" or "a!=b".  Here, a and b are lowercase letters (not necessarily different) that represent one-letter variable names.

Return true if and only if it is possible to assign integers to variable names so as to satisfy all the given equations.

</p>



## Example Test Cases [Leetcode 990](https://leetcode.com/problems/satisfiability-of-equality-equations/)

```
Input: ["a==b","b!=a"]
Output: false
Explanation: If we assign say, a = 1 and b = 1, then the first equation is satisfied, but not the second.  There is no way to assign the variables to satisfy both equations.
```




## Problem Solutionn [Leetcode 990](https://leetcode.com/problems/satisfiability-of-equality-equations/)


```cpp
class Solution {
public:
    unordered_map<char, char> mp;
    
    char find(char a){
        if(mp[a] != a) mp[a] = find(mp[a]);
        return mp[a];
    }
    bool equationsPossible(vector<string>& equations) {
        for(string s : equations){
            char a = s[0], b = s[3];
            if(!mp.count(a)) mp[a] = a;
            if(!mp.count(b)) mp[b] = b;
        }
        
        for(string s : equations){
            if(s[1] == '='){
                char a = s[0], b = s[3];
                char pa = find(a), pb = find(b);
                if(pa != pb) mp[pa] = pb;
            }
        }
        
        for(string s : equations){
            if(s[1] == '!'){
                char a = s[0], b = s[3];
                char pa = find(a), pb = find(b);
                if(pa == pb) return false;
            }
        }
        
        return true;
    }
};
```



