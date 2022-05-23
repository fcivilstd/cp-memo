---
tags:
    - 区間スケジューリング
    - 分数の比較
---

# ABC225-E

[問題](https://atcoder.jp/contests/abc225/tasks/abc225_e)

## 考察

「フ」の範囲を傾きで表したとき、区間スケジューリング問題に帰着できる。区間スケジューリングにおける、大小関係の判定は工夫して整数で行うと誤差が生じない。

## 計算量

区間スケジューリング：O(NlogN)
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
 
    vi x(n), y(n);
    rep(i, n) cin >> x[i] >> y[i];
 
    vi ids(n);
    rep(i, n) ids[i] = i;
 
    sort(all(ids), [&](int i, int j){
        return (ll)y[i] * (x[j] - 1) < (ll)y[j] * (x[i] - 1);
    });
 
    int ans = 0;
    // first / second
    pii pre = make_pair(0, 1);
    rep(i, n) {
        if ((ll)pre.first * x[ids[i]] > (ll)(y[ids[i]] - 1) * pre.second) continue;
        ans++;
        pre = make_pair(y[ids[i]], x[ids[i]] - 1);
    }
 
    cout << ans << endl;
 
    return 0;
}
```
