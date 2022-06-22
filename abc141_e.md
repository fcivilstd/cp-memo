---
tags:
    - 動的計画法
    - Z-algorithm
---

# ABC141-E

[問題](https://atcoder.jp/contests/abc141/tasks/abc141_e)

## 考察

dp\[i]\[j] := iからとjから始めた部分文字列が何文字一致しているか
このようなDP配列をつくると、遷移は
dp\[i]\[j] += dp\[i - 1]\[j - 1] (s\[i] == s\[j]のとき)
となる。1-indexedであれば配列外参照しない。

別解として、各部分文字列S.substr(i)(ただし、i = i...n - 1)に対してZ-algorithmを適用してもよい。

## 計算量

## コーディング

DP配列

```cpp
// #define _GLIBCXX_DEBUG
#include<bits/stdc++.h>

#define rep(i, n) for (int i = 0; i < (int)(n); i++)
#define rng(i, a, b) for (int i = (int)(a); i < (int)(b); i++)
#define rrng(i, a, b) for (int i = (int)(b) - 1; i >= (int)(a); i--)
#define all(x) x.begin(), x.end()
#define rall(x) x.rbegin(), x.rend()

using namespace std;

using ll = long long;
using ull = unsigned long long;
using vi = vector<int>;
using vvi = vector<vector<int>>;
using pii = pair<int, int>;

template<typename T, typename U>
inline bool chmax(T &x, U y) {return x < y ? (x = y, true) : false;}
template<typename T, typename U>
inline bool chmin(T &x, U y) {return x > y ? (x = y, true) : false;}

// const int MOD = 1000000007;
// const int MOD = 998244353;

int dp[5005][5005];

int main()
{
    int n;
    cin >> n;

    string s;
    cin >> s;

    rng(i, 1, n + 1) rng(j, 1, n + 1) {
        if (s[i - 1] != s[j - 1]) continue;
        dp[i][j] = dp[i - 1][j - 1] + 1;
    }

    int ans = 0;
    rng(j, 1, n + 1) rng(i, 1, j) {
        chmax(ans, min(j - i, dp[i][j]));
    }

    cout << ans << endl;

    return 0;
}
```

Z-algorithm

```cpp
// #define _GLIBCXX_DEBUG
#include<bits/stdc++.h>

#define rep(i, n) for (int i = 0; i < (int)(n); i++)
#define rng(i, a, b) for (int i = (int)(a); i < (int)(b); i++)
#define rrng(i, a, b) for (int i = (int)(b) - 1; i >= (int)(a); i--)
#define all(x) x.begin(), x.end()
#define rall(x) x.rbegin(), x.rend()

using namespace std;

using ll = long long;
using ull = unsigned long long;
using vi = vector<int>;
using vvi = vector<vector<int>>;
using pii = pair<int, int>;

template<typename T, typename U>
inline bool chmax(T &x, U y) {return x < y ? (x = y, true) : false;}
template<typename T, typename U>
inline bool chmin(T &x, U y) {return x > y ? (x = y, true) : false;}

// const int MOD = 1000000007;
// const int MOD = 998244353;

vector<int> zalgorithm(string& str)
{
    int n = str.size();
    vector<int> ret(n);

    int s = -1, t = -1;
    for (int i = 1; i < n; i++) {
        if (s != -1) ret[i] = min(ret[i - s], max(0, t - i));
        while (i + ret[i] < n && str[ret[i]] == str[i + ret[i]]) ret[i]++;
        if (t < i + ret[i]) {
            s = i;
            t = i + ret[i];
        }
    }

    ret[0] = n;

    return ret;
}

int main()
{
    int n;
    cin >> n;

    string s;
    cin >> s;

    int ans = 0;
    rep(i, n) {
        string sb = s.substr(i);
        auto z = zalgorithm(sb);
        rep(j, z.size()) chmax(ans, min(z[j], j));
    }

    cout << ans << endl;

    return 0;
}
```
