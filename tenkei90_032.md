---
tags:
    - 全探索
    - 順列全探索
    - 言語知識
---

# 典型90-032

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_af)

## 考察

並びを全探索するには、next_permutationを使えばよい。
噂を一つ一つ検証してもこの問題の制約では十分高速に解を得られる。

## 計算量

順列全探索：O(N!)
噂の検証：O(N)
よって、総計算量は
O(N! * N)

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

const int mx = 100100100;

int main()
{
    int n;
    cin >> n;

    vector<vector<int>> a(n, vector<int>(n));
    rep(i, n) rep(j, n) cin >> a[i][j];

    int m;
    cin >> m;

    vector<vector<int>> c(n, vector<int>(n));
    rep(i, m) {
        int x, y;
        cin >> x >> y;
        x--; y--;
        c[x][y] = 1;
        c[y][x] = 1;
    }

    vector<int> idx(n);
    rep(i, n) idx[i] = i;

    auto f = [&](){
        rep(j, n - 1) {
            if (c[idx[j]][idx[j + 1]]) return false;
        }
        return true;
    };

    int ans = mx;
    do {
        if (!f()) continue;
        int sum = 0;
        rep(i, n) sum += a[idx[i]][i];
        chmin(ans, sum);
    } while (next_permutation(all(idx)));

    if (ans != mx) cout << ans << endl;
    else cout << -1 << endl;

    return 0;
}
```
