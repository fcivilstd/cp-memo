---
tags:
    - 三角比
---

# 典型90-018

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_r)

## 考察

頑張って三角比を使って計算する。

## 計算量

質問の受け取り：O(Q)
俯角の計算：O(1)
よって、総計算量は
O(Q)

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

const double pi = acos(-1);

int main()
{
    int t, l, x, y, q;
    cin >> t >> l >> x >> y >> q;

    rep(i, q) {
        int e;
        cin >> e;

        double a, b;
        double ang = (double)2 * pi * (double)(e % t) / (double)t;
        
        a = sqrt(pow((double)x, 2) + pow((double)y - ((double)l / 2 * -cos(ang + pi * 3 / 2)), 2));
        b = (double)l / 2 * sin(ang + pi * 3 / 2) + (double)l / 2;

        cout << fixed << setprecision(10) << atan(b / a) * (double)180 / pi << endl;
    }

    return 0;
}
```
