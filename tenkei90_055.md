---
tags:
    - 全探索
---

# 典型90-055

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_bc)

## 考察

全探索をしても、定数倍が軽いため実行時間制限内に解を得ることができる。

## 計算量

全探索：O(N^5)
よって、総計算量は
O(N^5)

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
    int n, p, q;
    cin >> n >> p >> q;

    vector<int> a(n);
    rep(i, n) cin >> a[i];

    int ans = 0;
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            for (int k = j + 1; k < n; k++) {
                for (int l = k + 1; l < n; l++) {
                    for (int m = l + 1; m < n; m++) {
                        ll t = 1;
                        (t *= (ll)a[i]) %= p;
                        (t *= (ll)a[j]) %= p;
                        (t *= (ll)a[k]) %= p;
                        (t *= (ll)a[l]) %= p;
                        (t *= (ll)a[m]) %= p;
                        if (t == q) ans++;
                    }
                }
            }
        }
    }

    cout << ans << endl;

    return 0;
}
```
