---
tags:
    - 二分探索
    - クエリ
---

# ABC248-D

[問題](https://atcoder.jp/contests/abc248/tasks/abc248_d)

## 考察

愚直に考えると、ALからARまでに含まれるXの数を数えると解を得ることができるが、この問題の制約では厳しい。左端からL番目までに含まれるXの数と左端からR+1番目までに含まれるXの数が分かればよいことから、二分探索を用いることで効率的に解を得られることに気づける。

## 計算量

二分探索：O(logN)
クエリの受け取り：O(Q)
よって、総計算量は
O(QlogN)

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

    vector<vector<int>> a(n + 1);
    rep(i, n) {
        int ai;
        cin >> ai;
        a[ai].push_back(i);
    }

    int q;
    cin >> q;

    rep(i, q) {
        int l, r, x;
        cin >> l >> r >> x;
        l--; r--;

        auto itrl = lower_bound(all(a[x]), l);
        auto itrr = lower_bound(all(a[x]), r + 1);

        cout << itrr - itrl << endl;
    }

    return 0;
}
```
