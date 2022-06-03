---
tags:
    - bitDP
---

# ABC142=E

[問題](https://atcoder.jp/contests/abc142/tasks/abc142_e)

## 考察

今持っている鍵で空けられる宝箱の集合Sを2進数で管理しながら、まだ持っていない鍵を追加したときの集合に遷移してDPすればよい。

## 計算量

集合の探索：O(2^N)
鍵の追加：O(M)
よって、総計算量は
O((2^N)M)

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
    vvi c(m);
    rep(i, m) {
        cin >> a[i] >> b[i];
        rep(j, b[i]) {
            int ci;
            cin >> ci;
            ci--;
            c[i].push_back(ci);
        }
    }

    vi dp(1 << n, INF);
    dp[0] = 0;
    rep(ss, 1 << n) {
        if (dp[ss] == INF) continue;
        rep(i, c.size()) {
            int ts = ss;
            rep(j, c[i].size()) {
                ts |= 1 << c[i][j];
            }
            chmin(dp[ts], dp[ss] + a[i]);
        }
    }

    if (dp[(1 << n) - 1] == INF) cout << -1 << endl;
    else cout << dp[(1 << n) - 1] << endl;

    return 0;
}
```
