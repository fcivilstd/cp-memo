---
tags:
    - 整数論
    - 最大公約数
    - ユークリッドの互除法
---

# 典型90-022

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_v)

## 考察

全ての立方体にするためには、全ての辺がある値で割り切れる必要があり、その値を最大化することで操作が最小回数となるため、A、B、Cの最大公約数を求めれば良いことに気づける。

## 計算量

最大公約数の計算(ユークリッドの互除法)：O(log(min(a, b)))
よって、総計算量は
O(log(min(a, b)))

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
    ll a, b, c;
    cin >> a >> b >> c;

    ll g = gcd(gcd(a, b), c);

    cout << (a + b + c) / g - 3 << endl;

    return 0;
}
```
