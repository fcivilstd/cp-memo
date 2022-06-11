---
tags:
    - 動的計画法
    - 個数制限なしナップザック問題
---

# ABC153-E

[問題](https://atcoder.jp/contests/abc153/tasks/abc153_e)

## 考察

典型的なナップザック問題に帰着できる。
個数制限なしの場合、k個とる場合、同じ行にk - 1以下の情報が記録されていることを利用することで高速化できる。
この問題で、DP配列は
dp\[i]\[j] := i番目までの魔法を使って、体力をj以下減らすための最小魔力
遷移は、
dp\[i + 1]\[j] = min(dp\[i + 1]\[j], dp\[i]\[j])
dp\[i + 1]\[min(h, j + a\[i])] = min(dp\[i + 1]\[min(h, j + a\[i])], dp\[i + 1]\[j] + b\[i])

## 計算量

動的計画法：O(NH)
よって、総計算量は
O(NH)

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
    int h, n;
    cin >> h >> n;

    vi a(n), b(n);
    rep(i, n) cin >> a[i] >> b[i];

    vi dp(h + 1, INF);
    dp[0] = 0;
    rep(i, n) {
        vi _dp(h + 1, INF);
        swap(dp, _dp);
        rep(j, h + 1) {
            dp[j] = min(_dp[j], dp[j]);
            dp[min(h, j + a[i])] = min(dp[min(h, j + a[i])], dp[j] + b[i]);
        }
    }

    cout << dp[h] << endl;

    return 0;
}
```
