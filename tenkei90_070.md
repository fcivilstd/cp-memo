---
tags:
    - マンハッタン距離
---

# 典型90-070

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_br)

## 考察

不便さが最小となる発電所の座標を(x, y)としたとき、不便さは
|x1 - x| + |y1 - y| + |x2 - x| + |y2 - y| + ...
=|x1 - x| + |x2 - x| + |y1 - y| + |y2 - y| + ...
となり、xとyは独立して考えられる。そして、x、yそれぞれについて不便さが最小となるのは、
x、yそれぞれの中央値を選んだ場合である。

## 計算量

ソート：(NlogN)
よって、総計算量は
O(NlogN)

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
    int n;
    cin >> n;

    vector<int> x(n), y(n);
    rep(i, n) {
        int xi, yi;
        cin >> xi >> yi;
        x[i] = xi;
        y[i] = yi;
    }

    sort(all(x));
    sort(all(y));

    int _x = x[n / 2];
    int _y = y[n / 2];

    ll ans = 0;
    rep(i, n) {
        ans += abs(x[i] - _x);
        ans += abs(y[i] - _y);
    }

    cout << ans << endl;

    return 0;
}
```
