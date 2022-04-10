---
tags:
    - 言語知識
---

# 典型90-061

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_bi)

## 考察

前後からのpushおよびpop、ランダムアクセスは、dequeを使用すればよい。

## 計算量

クエリの受け取り：O(Q)
dequeへの挿入：O(1)
dequeへのランダムアクセス：O(1)
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
    int q;
    cin >> q;

    deque<int> d;
    rep(i, q) {
        int t, x;
        cin >> t >> x;

        if (t == 1) {
            d.push_front(x);
        } else if (t == 2) {
            d.push_back(x);
        } else {
            cout << d[x - 1] << endl;
        }
    }

    return 0;
}
```
