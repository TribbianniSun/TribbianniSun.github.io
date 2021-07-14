# Leetcode_162 Find Peak Element



Use **binary-search** to solve Leetcode_162 Find Peak Element.
<!--more-->

## Problem Solution [162. Find Peak Element](https://leetcode.com/problems/find-peak-element/)

```cpp
class Solution {
public:

    int findPeakElement(const vector<int> &num) {
        return Helper(num, 0, num.size()-1);
    }
    int Helper(const vector<int> &num, int low, int high)
    {
        if(low == high)
            return low;
        else
        {
            int mid1 = (low+high) / 2;
            int mid2 = mid1 + 1;
            if(num[mid1] < num[mid2])
                return Helper(num, mid2, high);
            else
                return Helper(num, low, mid1);
        }
    }
};
```
