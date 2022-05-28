---
tags:
    - 全探索
    - DFS
    - 排他的論理和
---

# ABC236-D

[問題](https://atcoder.jp/contests/abc236/tasks/abc236_d)

## 考察

ダブりなく全探索する方法を考える。1人目を固定しながら考えられる2人目を再帰で探索するとダブらない。
また、bitDPでも解けそうな雰囲気をしている。採用したペアを集合に足していきながら遷移させるという方法である。しかし、排他的論理和の性質上、最大値からの遷移が最大値になるとは限らないため、この解法は間違いである。

## 計算量

全探索：O(N!!)

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

int n, ans = 0;
vvi a;
void dfs(int s, int x)
{
    int si = -1;
    rep(i, 2 * n) if (!(s & (1 << i))) {si = i; break;}
    if (si == -1) chmax(ans, x);

    rng(sj, si + 1, 2 * n) {
        if (!(s & (1 << sj))) dfs(s | (1 << si) | (1 << sj), x ^ a[si][sj]);
    }
}

int main()
{
    cin >> n;

    a = vvi(2 * n, vi(2 * n));
    rep(i, 2 * n) rep(j, 2 * n) {
        if (i >= j) continue;
        cin >> a[i][j];
    }

    dfs(0, 0);

    cout << ans << endl;

    return 0;
}
```
