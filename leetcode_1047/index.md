# Leetcode_1047 Remove All Adjacent Duplicates In String


Use **stack** to solve Leetcode 1047 Remove All Adjacent Duplicates In String.
<!--more-->


## Problem Description [Leetcode 1047 - Count Different Palindromic Subsequences](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/)

<p>
You are given a string s consisting of lowercase English letters. A duplicate removal consists of choosing two adjacent and equal letters and removing them.

We repeatedly make duplicate removals on s until we no longer can.

Return the final string after all such duplicate removals have been made. It can be proven that the answer is unique.
</p>



## Example Test Cases [Leetcode 1047 - Count Different Palindromic Subsequences](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/)

```
Input: s = "abbaca"
Output: "ca"
Explanation: 
For example, in "abbaca" we could remove "bb" since the letters are adjacent and equal, and this is the only possible move.  The result of this move is that the string is "aaca", of which only "aa" is possible, so the final string is "ca".
```

## Problem Solution [Leetcode 1047 - Count Different Palindromic Subsequences](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/)
```cpp
typedef pair<char, int> PCI;

class Solution {
public:
    string removeDuplicates(string s) {
        return removeDuplicates(s, 2);
        
    }
    
    string removeDuplicates(string s, int k) {
        stack<PCI> myStack;
        for(int i = 0; i < s.size(); i++){
            if(myStack.size() and myStack.top().first == s[i]){
                myStack.top().second += 1;
            }
            else{
                myStack.push({s[i], 1});
            }
            while(myStack.size() and myStack.top().second >= k){
                myStack.top().second %= k;
                if(!myStack.top().second) myStack.pop();
            }
        }
        vector<char> ret;
        while(myStack.size()){
            auto it = myStack.top(); myStack.pop();
            for(int i = 0; i < it.second; i++) ret.push_back(it.first);
        }
        reverse(ret.begin(), ret.end());
        return string(ret.begin(), ret.end());
    }
};
```




