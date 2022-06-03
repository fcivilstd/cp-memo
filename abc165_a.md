---
tags:
    - 倍数の性質
    - 整数論
---

# ABC165-A

[問題](https://atcoder.jp/contests/abc165/tasks/abc165_a)

## 考察

X以下の最大のKの倍数は、
floor(X / K) * k
で求められる。

## 計算量

総計算量はO(1)

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
using vi = vector<int>;
using vvi = vector<vector<int>>;
using pii = pair<int, int>;

template<typename T, typename U>
inline bool chmax(T &x, U y) {return x < y ? (x = y, true) : false;}
template<typename T, typename U>
inline bool chmin(T &x, U y) {return x > y ? (x = y, true) : false;}

// const int MOD = 1000000007;
// const int MOD = 998244353;

int main()
{
    int k, a, b;
    cin >> k >> a >> b;

    int c = (b / k) * k;
    if (a <= c) {
        cout << "OK" << endl;
    } else {
        cout << "NG" << endl;
    }

    return 0;
}
```
