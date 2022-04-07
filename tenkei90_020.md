---
tags:
    - 式変形
---

# 典型90-020

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_t)

## 考察

大小関係の比較は、浮動小数点数のまま扱うと誤差によって誤った判定をしてしまう可能性があるため、式変形を上手く行って整数で処理する。

## 計算量

大小の判定：O(1)
O(1)

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

ll f(ll x, ll n)
{
    ll ret = 1;
    while (n--) {
        ret *= x;
    }
    return ret;
}

int main()
{
    ll a, b, c;
    cin >> a >> b >> c;

    if (a < f(c, b)) cout << "Yes" << endl;
    else cout << "No" << endl;

    return 0;
}
```
