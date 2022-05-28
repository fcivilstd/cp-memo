---
tags:
    - LIS
---

# ARC126-B

[問題](https://atcoder.jp/contests/arc126/tasks/arc126_b)

## 考察

選択した線分のaが昇順でかつbが昇順であれば、線分は交差しない。線分の本数を最大化するためには、aでソートした後にbの最長増加部分列(LIS)を求めればよい。

## 計算量

LIS：O(MlogM)

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

const int INF = 1 << 30;

int main()
{
    int n, m;
    cin >> n >> m;

    vi a(m), b(m);
    rep(i, m) cin >> a[i] >> b[i];

    vi ids(m);
    rep(i, m) ids[i] = i;

    sort(all(ids), [&](int i, int j){
        if (a[i] != a[j]) return a[i] < a[j];
        else return b[i] > b[j];
    });

    vi dp(m, INF);
    rep(i, m) {
        *lower_bound(all(dp), b[ids[i]]) = b[ids[i]];
    }

    cout << lower_bound(all(dp), INF) - dp.begin() << endl;

    return 0;
}
```
