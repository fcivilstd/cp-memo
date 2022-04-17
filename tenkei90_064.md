---
tags:
    - 未分類
---

# 典型90-064

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_bl)

## 考察

愚直に考えると、標高が変化した区間全てを更新して、不便さを計算し直せば解を得ることができるが、この問題の制約では厳しい。
地殻変動で標高が変化しても、変化する区間の両端のみで不便さが変化することから、地殻変動で更新するのは2箇所だけでよいことに気づける。

## 計算量

クエリの受け取り：O(Q)
不便さの更新：O(1)
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

int main()
{
    int n, q;
    cin >> n >> q;

    ll ans = 0;
    vector<ll> a(n), b(n - 1);
    rep(i, n) cin >> a[i];
    rep(i, n - 1) {
        b[i] = a[i] - a[i + 1];
        ans += abs(b[i]);
    }

    while (q--) {
        int l, r, v;
        cin >> l >> r >> v;
        l--; r--;
        if (l != 0) {
            ans -= abs(b[l - 1]);
            b[l - 1] -= v;
            ans += abs(b[l - 1]);
        }
        if (r != n - 1) {
            ans -= abs(b[r]);
            b[r] += v;
            ans += abs(b[r]);
        }
        cout << ans << endl;
    }

    return 0;
}
```
