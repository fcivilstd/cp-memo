---
tags:
    - コーナーケース
---

# 典型90-033

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_ag)

## 考察

wかhが1である場合は、どんな点灯の仕方をしても不適切でないため、全てのマスを点灯させることで解を得ることができる。
wもhも2以上である場合は、2で切り上げてかけ合わせると解を得ることができる。

## 計算量

最大値の計算：O(1)
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

int main()
{
    int h, w;
    cin >> h >> w;

    if (h < 2 || w < 2) {
        cout << h * w << endl;
        return 0;
    }

    int x = (h + 1) / 2;
    int y = (w + 1) / 2;

    cout << x * y << endl;

    return 0;
}
```
