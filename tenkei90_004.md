---
tags:
    - 前計算
---

# 典型90-004

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_d)

## 考察

愚直に考えると、各マスが属する行と列の合計値を求める必要があるが、計算量はO(HW(H + W))となり、この問題の制約では厳しい。
各マスの最終的な出力は、(行の合計値) + (列の合計値) - (そのマスの値)であるから、各行の合計値と各列の合計値を前計算しておけばよいことに気づける。

## 計算量

各行の合計値を求める：O(H)
各列の合計値を求める：O(W)
よって、総計算量は
O(HW)

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

    vector<vector<int>> a(h, vector<int>(w));
    vector<int> r(h), c(w);
    rep(i, h) rep(j, w) {
        cin >> a[i][j];
        r[i] += a[i][j];
        c[j] += a[i][j];
    }

    rep(i, h) rep(j, w) cout << r[i] + c[j] - a[i][j] << " \n"[j == w - 1];
    
    return 0;
}
```
