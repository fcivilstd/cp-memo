---
tags:
    - 動的計画法
    - 桁DP
---

# ABC154-E

[問題](https://atcoder.jp/contests/abc154/tasks/abc154_e)

## 考察

基本的な桁DPをする。

## 計算量

## コーディング

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

int dp[110][5][2];

int main()
{
    string s; int k;
    cin >> s >> k;

    dp[0][0][0] = 1;
    rep(i, s.size()) {
        // 0 -> 0
        if (s[i] == '0') rep(j, k + 1) dp[i + 1][j][0] += dp[i][j][0];
        else rep(j, k + 1) dp[i + 1][j + 1][0] += dp[i][j][0];

        // 0 -> 1
        int si = s[i] - '0';
        rng(_, 1, si) rep(j, k + 1) dp[i + 1][j + 1][1] += dp[i][j][0];
        if (si) rep(j, k + 1) dp[i + 1][j][1] += dp[i][j][0];

        // 1 -> 1
        rng(_, 1, 10) rep(j, k + 1) dp[i + 1][j + 1][1] += dp[i][j][1];
        rep(j, k + 1) dp[i + 1][j][1] += dp[i][j][1];
    }

    cout << dp[s.size()][k][0] + dp[s.size()][k][1] << endl;

    return 0;
}
```
