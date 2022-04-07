---
tags:
    - 累積和
    - imos法
---

# 典型90-028

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_ab)

## 考察

愚直に考えると、長方形の面積を塗り潰して後から重なっているマスを数えると解が得られるが、各紙毎に面積分塗りつぶすつとO(Nxy)となりこの問題の制約では厳しい。
imos法を使えば塗りつぶす面積が縁だけになるため高速化が可能である。

## 計算量

縁を塗る：O(x or y)
面積の計算：O(xy)
よって、総計算量は
O(Nx + xy or Ny + xy)

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

    vector<vector<int>> a(1010, vector<int>(1010));
    rep(i, n) {
        int lx, ly, rx, ry;
        cin >> lx >> ly >> rx >> ry;

        for (int j = ly; j < ry; j++) {
            a[j][lx]++;
            a[j][rx]--;
        }
    }

    vector<int> ans(n + 1);
    rep(i, a.size()) {
        rep(j, a[i].size()) {
            if (j) {
                a[i][j] += a[i][j - 1];
            }
            ans[a[i][j]]++;
        }
    }

    rng(i, 1, n + 1) cout << ans[i] << endl;

    return 0;
}
```
