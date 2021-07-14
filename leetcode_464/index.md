# Leetcode_464. Can I Win



Use **DFS, bitmask** to solve Leetcode 464. Can I Win
<!--more-->


## Problem Description [Leetcode 464. Can I Win](https://leetcode.com/problems/can-i-win/)

<p>
In the "100 game" two players take turns adding, to a running total, any integer from 1 to 10. The player who first causes the running total to reach or exceed 100 wins.

What if we change the game so that players cannot re-use integers?

For example, two players might take turns drawing from a common pool of numbers from 1 to 15 without replacement until they reach a total >= 100.

Given two integers maxChoosableInteger and desiredTotal, return true if the first player to move can force a win, otherwise, return false. Assume both players play optimally.
</p>

## Example Test Cases [Leetcode 464. Can I Win](https://leetcode.com/problems/can-i-win/)

```
Input: maxChoosableInteger = 10, desiredTotal = 11
Output: false
Explanation:
No matter which integer the first player choose, the first player will lose.
The first player can choose an integer from 1 up to 10.
If the first player choose 1, the second player can only choose integers from 2 up to 10.
The second player will win by choosing 10 and get a total = 11, which is >= desiredTotal.
Same with other integers chosen by the first player, the second player will always win.
```

## Problem Solution [Leetcode 464. Can I Win](https://leetcode.com/problems/can-i-win/)



### DFS + Bitmask + DP (raw)

```cpp
class Solution {
public:
    
    unordered_map<int, int> mp;
    

    //
    // state -> state of the game, 1 means picked, 0 means not picked
    // c -> current sum
    // d -> target sum
    // m -> maxChoosableInteger

    bool canIWinHelper(int state, int c, int d, int m){
        int k = (state << 9) + c;
        
        if(mp.count(k)) return mp[k];
        
        int ret = 0;
        
        for(int i = m; i >= 1; i--){
            if(state & 1 << i) continue;
            
            if(c + i >= d){
                ret = 1;
                break;
            }
            
            if(!canIWinHelper(state + (1 << i), c + i, d, m)){
                ret = 1;
                break;
            }
        }
        return mp[k] = ret;   
    }
    
    bool canIWin(int maxChoosableInteger, int desiredTotal) {
        if((maxChoosableInteger * (maxChoosableInteger + 1)) / 2 < desiredTotal){
            return false;
        }
        return canIWinHelper(0, 0, desiredTotal, maxChoosableInteger);
    }
};
```


### DFS + Bitmask + DP (optimized)

<p>we actually realize that when the state of the game is set, we also know the information of the currentSum; therefore, there is no need for us to add currentsum as part of the unordered_map.

More specifically, one state corresponds to one unique current sum, therefore, the search space for raw is the same with optimized. However, if we can only store states, array is much faster than unordered_map
</p>

```cpp
class Solution {
public:
    
    int mp[1 << 21];
    
    bool canIWinHelper(int state, int d, int m){
        
        if(mp[state] != -1) return mp[state];
        if(d <= 0) return mp[state] = 0;
        
        int ret = 0;
        
        for(int i = 1; i <= m; i++){
            if(state & 1 << i) continue;
            
            if(!canIWinHelper(state + (1 << i), d - i, m)){
                ret = 1;
                break;
            }
        }
        return mp[state] = ret;   
    }
    
    bool canIWin(int maxChoosableInteger, int desiredTotal) {
        
        
        if(desiredTotal < 2) return true;
        if((maxChoosableInteger * (maxChoosableInteger + 1)) / 2 < desiredTotal){
            return false;
        }
        
        memset(mp, -1, sizeof mp);
        return canIWinHelper(0, desiredTotal, maxChoosableInteger);
    }
};
```



