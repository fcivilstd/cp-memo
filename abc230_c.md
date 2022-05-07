---
tags:
    - マンハッタン距離
---

# ABC230-C

[問題](https://atcoder.jp/contests/abc230/tasks/abc230_c)

## 考察

グリッド上を斜め移動するとは、マンハッタン距離が一定になるように移動すると言い換えられる。この言い換えによって、移動中の座標にkを含まないことができる。

X = (A + k) - (B + k) = A - B
Y = (A + k) + (B - k) = A + B

今考えている座標(X, Y)に対して、X - Y = A - B または X + Y = A + Bが成り立つかどうかの判定を行えばよい。

## 計算量

座標の判定：O(1)
グリッド上の探索：O((Q - P + 1) \* (S -  R + 1))
よって、総計算量は
O((Q - P + 1) \* (S -  R + 1))

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
    ll n, a, b, p, q, r, s;
    cin >> n >> a >> b >> p >> q >> r >> s;

    vector<vector<char>> g(q - p + 1, vector<char>(s - r + 1, '.'));

    for (ll i = 0; i < q - p + 1; i++) {
        for (ll j = 0;  j < s - r + 1; j++) {
            ll x = p + i;
            ll y = r + j;
            if (x - y == a - b || x + y == a + b) g[i][j] = '#';
        }
    }

    for (ll i = 0; i < q - p + 1; i++) {
        for (ll j = 0;  j < s - r + 1; j++) {
            cout << g[i][j];
            if (j == s - r) cout << endl;
        }
    }

    return 0;
}
```
