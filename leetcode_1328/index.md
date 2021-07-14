# Leetcode 1328. Break a Palindrome


Use **Greedy** to solve Leetcode 1328 - Break a Palindrome.
<!--more-->

## Problem Solution [Leetcode 1328. Break a Palindrome](https://leetcode.com/problems/break-a-palindrome/)

```cpp
class Solution {
public:
    string breakPalindrome(string palindrome) {
        if(palindrome.size() <= 1) return "";
        
        for(int i = 0; i < palindrome.size() / 2; i++){
            if(palindrome[i] != 'a'){
                return palindrome.substr(0, i) + "a" + palindrome.substr(i + 1);
            }
        }
        
        for(int i = palindrome.size() - 1; i > palindrome.size() / 2; i--){
            if(palindrome[i] != 'a'){
                return palindrome.substr(0, i) + "a" + palindrome.substr(i + 1);
            }
        }
        int n = palindrome.size();
        return palindrome.substr(0, n - 1) + "b";
    }
};
```
