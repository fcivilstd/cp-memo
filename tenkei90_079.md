---
tags:
    - 未分類
---

# 典型90-079

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_ca)

## 考察

グリッドの左上から0になるように操作を行えば解を得ることができる。

## 計算量

グリッドの全探索：O(HW)
よって、総計算量は
O(HW)

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

template<typename T, typename U>
inline bool chmax(T &x, U y) {return x < y ? (x = y, true) : false;}
template<typename T, typename U>
inline bool chmin(T &x, U y) {return x > y ? (x = y, true) : false;}

// const int MOD = 1000000007;
// const int MOD = 998244353;

int main()
{
    int h, w;
    cin >> h >> w;

    vector<vector<ll>> a(h, vector<ll>(w)), b(h, vector<ll>(w));
    rep(i, h) rep(j, w) cin >> a[i][j];
    rep(i, h) rep(j, w) cin >> b[i][j];

    ll ans = 0;
    rep(i, h) rep(j, w) a[i][j] -= b[i][j];
    rep(i, h - 1) rep(j, w - 1) {
        ll t = a[i][j];
        ans += abs(t);
        a[i][j] -= t;
        a[i][j + 1] -= t;
        a[i + 1][j] -= t;
        a[i + 1][j + 1] -= t;
    }

    bool flag = true;
    rep(i, h) rep(j, w) if (a[i][j]) flag = false;

    if (flag) {
        cout << "Yes" << endl;
        cout << ans << endl;
    } else {
        cout << "No" << endl;
    }

    return 0;
}
```
