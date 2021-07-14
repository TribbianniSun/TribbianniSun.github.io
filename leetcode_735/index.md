# Leetcode_735. Asteroid Collision


Use **stack** to solve Leetcode 735. Asteroid Collision.
<!--more-->


## Problem Solution [Leetcode 735. Asteroid Collision](https://leetcode.com/problems/asteroid-collision/)

```cpp
class Solution {
public:
    vector<int> asteroidCollision(vector<int>& asteroids) {
        vector<int> ret;
        for(int i = 0; i < asteroids.size(); i++){
            int a = asteroids[i];
            if(ret.size() == 0 or ret.back() * a > 0 or a > 0) ret.push_back(a);
            else if(ret.back() == -a) ret.pop_back();
            else if(abs(ret.back()) < abs(a)){
                ret.pop_back();
                i -= 1;
            }
            else {
                continue;
            }
        }
        return ret;
    }
};
```
