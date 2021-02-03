# OJ Practice 5


OJ Practice 5, share my solutions for these three OJ problems during the UCSD ICPC Selection Contest.
<!--more-->

## Problem Solution to [Methodic Multiplication](https://vjudge.net/problem/Kattis-methodicmultiplication)

```cpp
#include <cstdio>
#include <algorithm>
#define fastIO                        \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0)
#define INF 1e12
using namespace std;

int countS(string s){
    int ret = 0;
    for(int i = 0; i < s.length(); i++){
        if(s[i] == 'S'){
            ret += 1;
        }
    }
    return ret;
}
int main()
{

    string s1, s2;
    cin >> s1 >> s2;
    if(s1 == "0"){
        cout << "0";
    }
    else if(s2 == "0"){
        cout << "0";
    }
    else{
        int count1 = countS(s1), count2 = countS(s2);
        int ret = count1 * count2;
        int idx = 0;
        vector<char> resultS;
        for(int i = 0; i < ret; i++){
            resultS.push_back('S');
            resultS.push_back('(');
        }
        resultS.push_back('0');
        for(int i = 0; i < ret; i++){
            resultS.push_back(')');
        }
        string retS(resultS.begin(), resultS.end());
        cout << retS;
    }
    return 0;
}
```





## Problem Solution to [Dams in Distress](https://vjudge.net/problem/Kattis-damsindistress)

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
4 75
0 100 50
1 49 10
1 50 0
3 50 48
*/

int main()
{

    ll n, t;
    cin >> n >> t;

    unordered_map<int, vector<int>> graph;
    vector<ll> needed(n + 1, 0);
    vector<ll> require(n + 1, 0);
    vector<ll> current(n + 1, 0);

    // the first one need t amount of water
    needed[0] = t;
    require[0] = t;


    for(int i = 1; i <= n; i++){
        int d, c, u;
        cin >> d >> c >> u;
        // from parent to child
        if(graph.find(d) == graph.end()){
            graph[d] = vector<int> {i};
        }
        else{
            graph[d].push_back(i);
        }
        require[i] = c;
        current[i] = u;
    }
    
    deque<int> q;
    q.push_back(0);
    while(q.size()){
        int p = q.front();
        q.pop_front();
        if(graph.find(p) != graph.end()){
            for(int np : graph[p]){
                ll cur_n = max(needed[p], require[np]) - current[np];
                needed[np] = cur_n;
                q.push_back(np);
            }
        }
    }

    ll min_amount = LLONG_MAX;
    for(int i = 0; i <= n; i++){
        min_amount = min(min_amount, needed[i]);
    }
    cout << min_amount;
    /*TLE solution
    ll min_amount = LLONG_MAX;
    for(int i = 0; i <= n; i++){
        ll needed = require[i] - current[i];
        ll carry = require[i];
        int idx = i;
        while(idx != 0){
            int next_level = parent[idx];
            if(carry + current[next_level] < require[next_level]){
                break;
            }
            else{
                carry = carry + current[next_level];
                idx = parent[idx];
            }
        }
        if(idx == 0){
            min_amount = min(min_amount, needed);
        }
    }
    cout << min_amount;
    */
    
    return 0;
}
```



## Problem Solution to [Array of Discord](https://vjudge.net/problem/Kattis-arrayofdiscord)

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
3
2020 2020 2020
*/
/*
4
1 42 4711 9876
*/

ll magicSmall(ll num){
    if(num < 10){
        return 0;
    }
    else{
        string s = to_string(num);

        // if the first digit is not 1, we change it to 1, and return it.
        if(s[0] != '1'){
            s[0] = '1';
            return stoll(s);
        }
        // if the first digit is 1, we find the first non-zero, and change it to zero
        else{
            for(int i = 1; i < s.length(); i+=1){
                if(s[i] != '0'){
                    s[i] = '0';
                    return stoll(s);
                }
            }
        }
    }
    return num;
}

ll magicBig(ll num){
    if(num < 10){
        return 9;
    }
    else{
        string s = to_string(num);
        if(s[0] != '9'){
            s[0] = '9';
            return stoll(s);
        }
        // find the first non-9, and change it to 9
        else{
            for(int i = 1; i < s.length(); i+=1){
                if(s[i] != '9'){
                    s[i] = '9';
                    return stoll(s);
                }
            }
        }
    }
    return num;
}
int main()
{   
    int n;
    cin >> n;
    vector<ll> nums(n, 0);
    for(int i = 0; i < n; i++){
        ll num;
        cin >> num;
        nums[i] = num;
    }
    // either make left bigger, scan from the left to right, if the changed number is biggr than the one on the right,
    // we can return the array of numers
    for(int i = 0; i < nums.size() - 1; i++){
        if(magicBig(nums[i]) > nums[i+1]){
            nums[i] = magicBig(nums[i]);
            for(ll i : nums){
                cout << i << " ";
            }
            return 0;
        }
    }
    // or make right smaller, scan from right to left, if the changed number is smaller than the one on the left,
    // return the array of numbers
    for(int i = nums.size() - 1; i >= 1; i--){
        if(magicSmall(nums[i]) < nums[i - 1]){
            nums[i] = magicSmall(nums[i]);
            for(ll i : nums){
                cout << i << " ";
            }
            return 0;
        }
    }
    cout << "impossible";
    return 0;
}
```



## Problem Remark to [Array of Discord](https://vjudge.net/problem/Kattis-arrayofdiscord)
- Just use stoll, do not mess up with the overflow
