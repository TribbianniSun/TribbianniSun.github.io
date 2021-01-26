# OJ Practice 1


OJ Practice 1, share my solution for these three OJ problems.
<!--more-->

[NCPC 2013 Problem E: Timebomb](https://www.e-olymp.com/en/problems/6254)

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



int main()
{

    string s;
    vector<string> l;
    for(int i = 0; i < 5; ++i){
        std::getline (std::cin,s);
        l.push_back(s);
    }
    // for(string s : l){
    //     cout << s << endl;
    // }
    vector<string> num_str = {"75557", "11111", "71747", "71717", "55711", "74717", "74757", 
    "71111", "75757", "75717"};
    
    unordered_map<string, int> ref;
    for(int i = 0; i < num_str.size(); ++i){
        ref[num_str[i]] = i;
    }

    long long num = 0;
    vector<int> number;
    for(int i = 0; i < l[0].size(); i += 4){
        string s = "";
        for(int k = 0; k < 5; k++){
            int counter = 0;
            for(int j = 0; j < 3; j++){
                if(l[k][i + j] == '*'){
                    counter += pow(2, 2- j);
                }
            }
            s += to_string(counter);
        }
        if(ref.find(s) == ref.end()){
            cout << "BOOM!!";
            return 0;
        }
        else{
            number.push_back(ref[s]);
        }
    }

    for(int i = 0; i < number.size(); i += 1){
        num = num * 10 + number[i];
    }
    if(num % 6 == 0){
        cout << "BEER!!";
        return 0;
    }
    else{
        cout << "BOOM!!";
        return 0;
    }   
    return 0;
}
```


[NCPC 2015 Problem C: Cryptographer’s Conundrum](https://compprog.win.tue.nl:444/public/problems/186/text)


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

int solve(string s){
    int counter = 0;
    vector<char> ref = {'P', 'E', 'R'};
    for(int i = 0; i < s.length(); ++i){
        if(s[i] != ref[i % 3]){
            counter += 1;
        }
    }
    return counter;
}

int main()
{

    string s;
    cin >> s;
    cout << solve(s) << "\n";
    return 0;
}
```





[NCPC 2011 Problem E: ls](http://neerc.secna.ru/BOBROVKA_2012/day01/01.pdf)

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
*.*
4
main.c
a.out
readme
yacc
*/
bool solve(string s, string p){
    int s_len = s.length(), p_len = p.length();
    vector<vector<bool>> dp(s_len + 1, vector<bool>(p_len + 1, false));
    dp[0][0] = true;
    for(int j = 1; j <= p_len; ++j){
        if(p[j - 1] == '*'){
            dp[0][j] = dp[0][j-1];
        }
        else{
            dp[0][j] = false;
        }
    }
    for(int i = 1; i <= s_len; ++i){
        for(int j = 1; j <= p_len; ++j){
            if(p[j-1] == '*'){
                dp[i][j] = dp[i-1][j] || dp[i][j-1] || dp[i-1][j-1];
            }
            else{
                if(p[j-1] == s[i-1]){
                    dp[i][j] = dp[i-1][j-1];
                }
                else{
                    dp[i][j] = false;
                }
            }
        }
    }
    return dp[s_len][p_len];
}

int main()
{

    int n = 0;
    string p, s;
    cin >> p;
    cin >> n;
    vector<string> l;
    for(int i = 0; i < n; i++){
        cin >> s;
        if(solve(s, p)){
            l.push_back(s);
        }
    }
    for(string s : l){
        cout << s << endl;
    }
    return 0;
}
```
