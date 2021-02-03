# codeforce 1



codeforce Practice 1, share my solution for these this codeforce problem.
<!--more-->

## Problem Description [D. Cleaning the Phone](https://codeforces.com/problemset/problem/1475/D)

### Problem Introduction [D. Cleaning the Phone](https://codeforces.com/problemset/problem/1475/D)

<p>

Polycarp often uses his smartphone. He has already installed 𝑛 applications on it. Application with number 𝑖 takes up 𝑎𝑖 units of memory.

Polycarp wants to free at least 𝑚 units of memory (by removing some applications).

Of course, some applications are more important to Polycarp than others. He came up with the following scoring system — he assigned an integer 𝑏𝑖 to each application:

𝑏𝑖=1 — regular application;
𝑏𝑖=2 — important application.
According to this rating system, his phone has 𝑏1+𝑏2+…+𝑏𝑛 convenience points.

Polycarp believes that if he removes applications with numbers 𝑖1,𝑖2,…,𝑖𝑘, then he will free 𝑎𝑖1+𝑎𝑖2+…+𝑎𝑖𝑘 units of memory and lose 𝑏𝑖1+𝑏𝑖2+…+𝑏𝑖𝑘 convenience points.

For example, if 𝑛=5, 𝑚=7, 𝑎=[5,3,2,1,4], 𝑏=[2,1,1,2,1], then Polycarp can uninstall the following application sets (not all options are listed below):

applications with numbers 1,4 and 5. In this case, it will free 𝑎1+𝑎4+𝑎5=10 units of memory and lose 𝑏1+𝑏4+𝑏5=5 convenience points;
applications with numbers 1 and 3. In this case, it will free 𝑎1+𝑎3=7 units of memory and lose 𝑏1+𝑏3=3 convenience points.
applications with numbers 2 and 5. In this case, it will free 𝑎2+𝑎5=7 memory units and lose 𝑏2+𝑏5=2 convenience points.
Help Polycarp, choose a set of applications, such that if removing them will free at least 𝑚 units of memory and lose the minimum number of convenience points, or indicate that such a set does not exist.
<p>


### Problem Input [D. Cleaning the Phone](https://codeforces.com/problemset/problem/1475/D)
<p>
Input
The first line contains one integer 𝑡 (1≤𝑡≤104) — the number of test cases. Then 𝑡 test cases follow.

The first line of each test case contains two integers 𝑛 and 𝑚 (1≤𝑛≤2⋅105, 1≤𝑚≤109) — the number of applications on Polycarp's phone and the number of memory units to be freed.

The second line of each test case contains 𝑛 integers 𝑎1,𝑎2,…,𝑎𝑛 (1≤𝑎𝑖≤109) — the number of memory units used by applications.

The third line of each test case contains 𝑛 integers 𝑏1,𝑏2,…,𝑏𝑛 (1≤𝑏𝑖≤2) — the convenience points of each application.

It is guaranteed that the sum of 𝑛 over all test cases does not exceed 2⋅105.
<p>


### Problem Output [D. Cleaning the Phone](https://codeforces.com/problemset/problem/1475/D)
<p>
Output
For each test case, output on a separate line:

-1, if there is no set of applications, removing which will free at least 𝑚 units of memory;
the minimum number of convenience points that Polycarp will lose if such a set exists.
<p>


### Example Input & Output [D. Cleaning the Phone](https://codeforces.com/problemset/problem/1475/D)

```
5
5 7
5 3 2 1 4
2 1 1 2 1
1 3
2
1
5 10
2 3 2 3 2
1 2 1 2 1
4 10
5 1 3 4
1 2 1 2
4 5
3 2 1 2
2 1 2 1
```


```
2
-1
6
4
3
```


### Example Explanation [D. Cleaning the Phone](https://codeforces.com/problemset/problem/1475/D)

```
In the first test case, it is optimal to remove applications with numbers 2 and 5, freeing 7 units of memory. 𝑏2+𝑏5=2.

In the second test case, by removing the only application, Polycarp will be able to clear only 2 of memory units out of the 3 needed.

In the third test case, it is optimal to remove applications with numbers 1, 2, 3 and 4, freeing 10 units of memory. 𝑏1+𝑏2+𝑏3+𝑏4=6.

In the fourth test case, it is optimal to remove applications with numbers 1, 3 and 4, freeing 12 units of memory. 𝑏1+𝑏3+𝑏4=4.

In the fifth test case, it is optimal to remove applications with numbers 1 and 2, freeing 5 units of memory. 𝑏1+𝑏2=3.
```

## Problem Solution [D. Cleaning the Phone](https://codeforces.com/problemset/problem/1475/D)

```cpp
#include <cstdio>
#include <algorithm>
#define fastIO                        \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0)
#define INF 1e12
using namespace std;


/*
5
5 7
5 3 2 1 4
2 1 1 2 1
1 3
2
1
5 10
2 3 2 3 2
1 2 1 2 1
4 10
5 1 3 4
1 2 1 2
4 5
3 2 1 2
2 1 2 1
*/


int main()
{

    int n;
    cin >> n;
    vector<ll> ret;
    for(int i = 0; i < n; i+=1){
        int m, needed;
        cin >> m >> needed;
        vector<ll> a(m + 1, 0);
        vector<int> b(m + 1, 0);
        vector<ll> _1;
        vector<ll> _2;
        ll sum = 0;
        for(int i = 1; i <= m; i++){
            cin >> a[i];
            sum += a[i];
        }
        for(int i = 1; i <= m; i++){
            cin >> b[i];
            if(b[i] == 1){
                _1.push_back(a[i]);
            }
            else{
                _2.push_back(a[i]);
            }
        }
        
        if(sum<needed) {
            ret.pb(-1);
            continue;
        }
        
        sort(_1.rbegin(), _1.rend());
        sort(_2.rbegin(), _2.rend());

        vector<ll> _pre2;
		_pre2.pb(0);

        for(int i = 0; i < _2.size(); i++){
            _pre2.push_back(_pre2[i] + _2[i]);
        }

        int len=_pre2.size();
        sum=0;
		ll ans=1e18;
        int cur=lower_bound(_pre2.begin(),_pre2.end(),needed)-_pre2.begin();

        // if cur == len, it means that no element inside the _pre2 >= needed
        if(cur!=len) {
            ans=cur*2;
        }

        for(int i = 0; i < _1.size(); i++){
            sum += _1[i];
            if(needed < 0){
                ans = min(ans, 1ll + i + 1);
                break;
            }
            int point = needed - sum;
            int cur=lower_bound(_pre2.begin(),_pre2.end(),point)-_pre2.begin();
            if(cur != len){
                ans = min(ans,  i + 1 + 2 * 1ll * cur);
            }
        } 
        ret.push_back(ans);
    }
    for(int i : ret){
        cout << i << '\n';
    }
    return 0;
}

```


## Problem Remark [D. Cleaning the Phone](https://codeforces.com/problemset/problem/1475/D)
- Implicit Binary Search
- Idea is computing the prefix sum and set the pointer at application with importance 1, and then do binary search to find the lower_bound for the application with importance of 2
