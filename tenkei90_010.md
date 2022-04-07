---
tags:
    - クエリ
    - 累積和
    - 前計算
---

# 典型90-010

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_j)

## 考察

愚直に考えると、L~Rまでの和を順に足していけば解が得られるが、この問題の制約では厳しい。
累積和を前計算しておけば、L~Rまでの和をO(1)で計算できる。

## 計算量

累積和の前計算：O(N)
質問の受け取り：O(Q)
L~Rまでの和の計算：O(1)
よって、総計算量は
O(N + Q)

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

    vector<vector<int>> sum(2, vector<int>(n + 1));
    rep(i, n) {
        int c, p;
        cin >> c >> p;
        c--;
        sum[c][i + 1] = sum[c][i] + p;
        sum[1 - c][i + 1] = sum[1 - c][i];
    }

    int q;
    cin >> q;

    rep(i, q) {
        int l, r;
        cin >> l >> r;
        l--;
        cout << sum[0][r] - sum[0][l] << ' ' << sum[1][r] - sum[1][l] << endl;
    }

    return 0;
}
```
