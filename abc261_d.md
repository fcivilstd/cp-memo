---
tags:
    - 動的計画法
---

# ABC261-D

[問題](https://atcoder.jp/contests/abc261/tasks/abc261_d)

## 考察

典型的なナップザック問題ではあるが、あり得ない遷移はしないように初期値を工夫する必要がある。

## 計算量

動的計画法：O(N^2)
よって、総計算量は
O(N^2)

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

int main()
{
    int n, m;
    cin >> n >> m;

    vi x(n);
    rep(i, n) cin >> x[i];

    map<int, int> bonus;
    int c, y;
    rep(i, m) cin >> c >> y, bonus[c] += y;

    vector<vector<ll>> dp(n + 1, vector<ll>(n + 1, -1));
    dp[0][0] = 0;
    rep(i, n) {
        rep(j, n) {
            if (dp[i][j] == -1) continue;
            chmax(dp[i + 1][j + 1], dp[i][j] + x[i] + bonus[j + 1]);
            chmax(dp[i + 1][0], dp[i][j]);
        }
    }

    ll ans = 0;
    rep(j, n + 1) chmax(ans, dp[n][j]);

    cout << ans << endl;

    return 0;
}
```
