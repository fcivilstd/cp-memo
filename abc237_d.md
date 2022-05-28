---
tags:
    - 言語知識
---

# ABC237-D

[問題](https://atcoder.jp/contests/abc237/tasks/abc237_d)

## 考察

連結リストは標準ライブラリを使用すればよい。

## 計算量

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
    int n;
    cin >> n;

    list<int> a{0};
    auto itr = a.end();
    rep(i, n) {
        char c;
        cin >> c;
        if (c == 'L') itr--;
        a.insert(itr, i + 1);
    }

    for (auto ai : a) cout << ai << endl;

    return 0;
}
```
