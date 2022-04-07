---
tags:
    - 全探索
---

# 典型90-016

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_p)

## 考察

愚直に考えると、全ての硬貨の枚数を全探索することで解が得られるが、この問題の制約では厳しい。
合計9999枚以下の硬貨でちょうどN円を支払うことができるため、A円硬貨とB円硬貨の枚数までなら全探索が可能である。A円硬貨とB円硬貨の枚数が定まれば、C円硬貨の枚数は1意に定まる。

## 計算量

最大枚数をX(ここではX=9999)として、
各硬貨の全探索：O(X)
よって、総計算量は
O(X^2)

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
    ll n, a, b, c;
    cin >> n >> a >> b >> c;

    int ans = 10000;
    for (int na = 0; na < 10000; na++) {
        for (int nb = 0; (na + nb) < 10000; nb++) {
            if ((n - a * na - b * nb) < 0) break;
            if ((n - a * na - b * nb) % c == 0) {
                chmin(ans, na + nb + (n - a * na - b * nb) / c);
            }
        }
    }

    cout << ans << endl;

    return 0;
}
```
