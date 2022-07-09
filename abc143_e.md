---
tags:
    - ワ―シャルフロイド法
---

# ABC143-E

[問題](https://atcoder.jp/contests/abc143/tasks/abc143_e)

## 考察

[ワ―シャルフロイド法の証明](http://algorithms.blog55.fc2.com/blog-entry-52.html)

N<=300なので、計算量はN^3までなら許容できる。ワ―シャルフロイド法を使用して全点対最短経路を求めた後、一回の給油で行ける頂点対に辺を貼ったグラフを作り直し、新しく作ったグラフ上で全点対最短経路を求めればよい。

## 計算量

ワ―シャルフロイド法：O(N^3)
よって、総計算量は
O(N^3)

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

const ll INF = 1LL << 60;

int main()
{
    int n, m, l;
    cin >> n >> m >> l;

    vector<vector<ll>> dist(n, vector<ll>(n, INF)), dist2;
    dist2 = dist;
    rep(i, n) dist[i][i] = dist2[i][i] = 0;

    rep(i, m) {
        int a, b, c;
        cin >> a >> b >> c;
        a--; b--;
        if (c > l) continue;
        chmin(dist[a][b], c);
        chmin(dist[b][a], c);
    }

    rep(k, n) rep(i, n) rep(j, n) chmin(dist[i][j], dist[i][k] + dist[k][j]);
    
    rep(j, n) rep(i, n) if (dist[i][j] <= l) dist2[i][j] = dist2[j][i] = 1;
    rep(k, n) rep(i, n) rep(j, n) chmin(dist2[i][j], dist2[i][k] + dist2[k][j]);

    int q;
    cin >> q;

    while (q--) {
        int s, t;
        cin >> s >> t;
        s--; t--;
        if (dist2[s][t] == INF) cout << -1 << endl;
        else cout << dist2[s][t] - 1 << endl;
    }

    return 0;
}
```
