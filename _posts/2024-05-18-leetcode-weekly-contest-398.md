---
layout: post
title: Leetcode Weekly Contest 398
date: 2024-05-18 22:16:32
description: this is what included tabs in a post could look like
tags: leetcode
categories: code
tabs: true
---

This is a post about [weekly contest 398](https://leetcode.com/contest/weekly-contest-398/).

## 3151. Special Array I

```python
class Solution:
    def isArraySpecial(self, nums: List[int]) -> bool:
        for i in range(len(nums) - 1):
            if nums[i] % 2 == nums[i + 1] % 2:
                return False
        return True
```

## 3152. Special Array II

```python
class Solution:
    def isArraySpecial(self, nums: List[int], queries: List[List[int]]) -> List[bool]:
        p = [0]
        for i in range(len(nums) - 1):
            if nums[i] % 2 == nums[i + 1] % 2:
                p.append(p[-1] + 1)
            else:
                p.append(p[-1])
        print(p)
        ret = []
        for [a, b] in queries:
            if p[b] == p[a]:
                ret.append(True)
            else:
                ret.append(False)

        return ret
```

## 3153. Sum of Digit Differences of All Pairs

```python
class Solution:
    def sumDigitDifferences(self, nums: List[int]) -> int:
        nums = [str(num) for num in nums]
        l = len(nums[0])
        mp = [{} for _ in range(l)]
        n = len(nums)
        for i in range(n):
            for j in range(len(nums[i])):
                mp[j][nums[i][j]] = mp[j].get(nums[i][j], 0) + 1

        ret = 0
        for j in range(l):
            local_ret = 0
            for k in mp[j]:
                cnt = mp[j][k]
                local_ret += (n - cnt) * cnt
            local_ret = local_ret // 2
            ret += local_ret

        return ret

```

## 3154. Find Number of Ways to Reach the K-th Stair

```python
class Solution:
    def waysToReachStair(self, k: int) -> int:
        N = 35
        c = [[0 for _ in range(N)] for _ in range(N)]
        for i in range(N):
            c[i][0] = 1
        for i in range(1, N):
            for j in range(1, i + 1):
                c[i][j] = c[i - 1][j] + c[i - 1][j - 1]

        ret = 0
        for i in range(N - 1):
            for j in range(i + 2):
                t = 1
                for p in range(i):
                    t += pow(2, p)
                t -= j
                if t == k:
                    print(i, j)
                    ret += c[i + 1][j]


        return ret
```
