# OJ Practice 4


OJ Practice 4, share my solution for these three OJ problems.
<!--more-->
[[NCPC 2011 Problem A: Car Trouble]](https://www.e-olymp.com/en/contests/3556/problems/28964)

```cpp
#include <cstdio>
#include <algorithm>
#include <cstring>
#include <cassert>
#include <sstream>
#include <numeric>
#include <climits>
#include <cctype>
#include <ctime>
#include <cmath>
#include <vector>
#include <string>
#include <queue>
#include <list>
#include <map>
#include <set>
#include <unordered_map>
#include <unordered_set>
#include <iostream>
#include <fstream>
using namespace std;
#define ll long long
#define pb push_back
#define pf push_front
#define mp make_pair
#define F first
#define S second
#define mod 1000000007
#define vl vector<ll>
#define vi vector<int>
#define pli pair<ll, int>
#define pil pair<int, ll>
#define vpil vector<pil>
#define vpli vector<pli>
#define ml map<ll, ll>
#define mi map<int, int>
#define m(a, b) map<a, b>
#define YesNo(f)               \
    if (f)                     \
    {                          \
        cout << "YES" << endl; \
    }                          \
    else                       \
    {                          \
        cout << "NO" << endl;  \
    }
#define setval(a, val) memset(a, val, sizeof(a))
#define fastIO                        \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0)
#define INF 1e12

//Definition for a binary tree node.
struct TreeNode
{
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

struct ListNode
{
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

/*
6
0 1 1
1 1 2
2 3 1 3 0
3 0
4 2 5 0
5 1 4
*/
set<int> solve(unordered_map<int, vector<int>>& graph){
    set<int> seen;
    if (graph.find(0) == graph.end()){
        return seen;
    }

    deque<int> q;
    q.push_back(0);

    while(q.size()){
        int cur = q.front();
        q.pop_front();
        seen.insert(cur);
        for(int j = 0; j < graph[cur].size(); ++j){
            if(seen.find(graph[cur][j]) == seen.end()){
                seen.insert(graph[cur][j]);
                q.push_back(graph[cur][j]);
            }
        }
    }
    return seen;

}


int main()
{

    int m, f, t, n;
    unordered_map<int, vector<int>> graph;
    unordered_map<int, vector<int>> reverse_graph;
    vector<int> all_road;

    cin >> m;

    for(int i = 0; i < m; i++){
        cin >> f;
        cin >> n;
        all_road.push_back(f);
        if(reverse_graph.find(t) == reverse_graph.end()){
            reverse_graph[f] = vector<int>{};
        }
        if(graph.find(f) == graph.end()){
            graph[f] = vector<int>{};
        }
        
        for(int j = 0; j < n; j++){
            cin >> t;
            graph[f].push_back(t);
            reverse_graph[t].push_back(f);
        }
    }

    // UNREACHABLE 
    vector<int> unreachable;

    // TRAPPED
    vector<int> trapped;

    set<int> not_trapped = solve(reverse_graph);
    set<int> not_unreachable = solve(graph);

    for(int i : all_road){
        if(not_unreachable.find(i) == not_unreachable.end()){
            unreachable.push_back(i);
        }

        if(not_trapped.find(i) == not_trapped.end()){
            trapped.push_back(i);
        }
    }


    if(trapped.size() == 0 && unreachable.size() == 0){
        cout << "NO PROBLEMS";
        return 0;
    }


    else{
        for(int i : trapped){
            cout << "TRAPPED " << i << endl; 
        }
        for(int i : unreachable){
            cout << "UNREACHABLE " << i << endl;
        }
    }
    return 0;
}
```



[NCPC 2015​ Goblin Garden Guards](https://nanti.jisuanke.com/t/A1804)

```cpp
#include <cstdio>
#include <algorithm>
#include <cstring>
#include <cassert>
#include <sstream>
#include <numeric>
#include <climits>
#include <cctype>
#include <ctime>
#include <cmath>
#include <vector>
#include <string>
#include <queue>
#include <list>
#include <map>
#include <set>
#include <unordered_map>
#include <unordered_set>
#include <iostream>
#include <fstream>
using namespace std;
#define ll long long
#define pb push_back
#define pf push_front
#define mp make_pair
#define F first
#define S second
#define mod 1000000007
#define vl vector<ll>
#define vi vector<int>
#define pli pair<ll, int>
#define pil pair<int, ll>
#define vpil vector<pil>
#define vpli vector<pli>
#define ml map<ll, ll>
#define mi map<int, int>
#define m(a, b) map<a, b>
#define YesNo(f)               \
    if (f)                     \
    {                          \
        cout << "YES" << endl; \
    }                          \
    else                       \
    {                          \
        cout << "NO" << endl;  \
    }
#define setval(a, val) memset(a, val, sizeof(a))
#define fastIO                        \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0)
#define INF 1e12

//Definition for a binary tree node.
struct TreeNode
{
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

struct ListNode
{
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

/*
5
0 0
100 0
0 100
100 100
50 50
1
0 0 50
*/
int main()
{
    int n, m;
    cin >> n;
    int x, y, r;
    vector<tuple<int, int>> g;
    vector<tuple<int, int, int>> s;

    for (int i = 0; i < n; i++)
    {
        cin >> x >> y;
        g.push_back(make_tuple(x, y));
    }

    cin >> m;
    for (int i = 0; i < m; i++)
    {
        cin >> x >> y >> r;
        s.push_back(make_tuple(x, y, r));
    }

    vector<vector<bool>> board(10000 + 5, vector<bool>(10000 + 5, true));

    /*TLE SOLUTION
    int ret = 0;
    for(int i = 0; i < n; i++){
        bool flag = true;
        int g_x = get<0>(g[i]), g_y = get<1>(g[i]);
        for(int j = 0; j < m; j++){
            int s_x = get<0>(s[j]), s_y = get<1>(s[j]), s_r = get<2>(s[j]);
            if( pow((g_x - s_x), 2) + pow((g_y - s_y), 2) <= pow(s_r, 2)){
                flag = false;
                break;
            }
        }   
        if(flag){
            ret += 1;
        }
    }
    */

    for (int j = 0; j < m; j++)
    {
        int s_x = get<0>(s[j]), s_y = get<1>(s[j]), s_r = get<2>(s[j]);
        for (int dx = -s_r; dx <= s_r; dx++)
        {
            for (int dy = -s_r; dy <= s_r; dy++)
            {
                if (s_x + dx >= 0 && s_x + dx < 10000 + 5 && s_y + dy >= 0 && s_y + dy < 10000 + 5)
                {
                    // double check the name of variables is correct
                    if (dx * dx + dy * dy <= s_r * s_r)
                    {
                        board[s_x + dx][s_y + dy] = false;
                    }
                }
            }
        }
    }

    int ret = 0;
    for (int i = 0; i < n; i++)
    {
        int g_x = get<0>(g[i]), g_y = get<1>(g[i]);
        if (board[g_x][g_y])
        {
            ret += 1;
        }
    }

    cout << ret;

    return 0;
}
```
