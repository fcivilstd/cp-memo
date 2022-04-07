---
tags:
    - 言語知識
---

# 典型90-026

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_aa)

## 考察

存在の高速な判定には、setかmapを用いると良い。

## 計算量

要素の追加：O(NlogN)
要素の検索：O(logN)
よって、総計算量は
O(NlogN)

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

    set<string> st;
    rep(i, n) {
        string s;
        cin >> s;
        if (st.count(s)) continue;
        else {
            st.insert(s);
            cout << i + 1 << endl;
        }
    }

    return 0;
}
```
