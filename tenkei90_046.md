---
tags:
    - 倍数と余り
---

# 典型90-046

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_at)

## 考察

愚直に考えると、(i, j, k)を全探索すれば解を得ることができるが、計算量はO(N^3)であり、この問題の制約では厳しい。
この問題では倍数であるかどうかの情報以外必要ないため、A、B、Cの値を予め46で割った余りとして扱えば、全探索できる数まで落とせる。

## 計算量

全探索：O(N'^3) (N' = 46)
よって、総計算量は
O(N'^3)

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

    vector<ll> a(46), b(46), c(46);
    rep(i, n) {
        int ai;
        cin >> ai;
        a[ai % 46]++;
    }
    rep(i, n) {
        int bi;
        cin >> bi;
        b[bi % 46]++;
    }
    rep(i, n) {
        int ci;
        cin >> ci;
        c[ci % 46]++;
    }

    ll ans = 0;
    rep(i, 46) rep(j, 46) rep(k, 46) {
        if ((i + j + k) % 46) continue;
        ans += a[i] * b[j] * c[k];
    }

    cout << ans << endl;

    return 0;
}
```
