---
tags:
    - LIS
    - LDS
---

# ABC134-E

[問題](https://atcoder.jp/contests/abc134/tasks/abc134_e)

## 考察

例えば、3 1 4 1 5の数列を考えると、
3 4 5
1
1
と並べていくと、行数が答えとなる。並べるときには、狭義単調増加できる列の最も末尾の数字が大きい行の最後に追加する。このシミュレーションを実装しても解を得ることができるが、行数は、最長広義単調減少部分列の長さとなるため、逆から見てLISを求めればよい。

## 計算量

LIS：O(NlogN)
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

const int INF = 1001001001;

int main()
{
    int n;
    cin >> n;

    vi a(n);
    rep(i, n) cin >> a[i];
    reverse(all(a));

    vi dp(n, INF);
    rep(i, n) {
        // 広義単調増加
        *upper_bound(all(dp), a[i]) = a[i];
    }

    int ans = lower_bound(all(dp), INF) - dp.begin();
    cout << ans << endl;

    return 0;
}
```
