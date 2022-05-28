---
tags:
    - ダイクストラ法
---

# ABC237-E

[問題](https://atcoder.jp/contests/abc237/tasks/abc237_e)

## 考察

負のコストを有するグラフにおいて、ダイクストラ法は計算量が指数関数的に増える。これは、一度確定した地点は二度と変更されないという前提が壊れるからである。具体的には、

〇　　0　　〇　　0　　〇

　　3   -7    2    -4

　　　〇　　　　　〇

といったケースである。負のコストを非負のコストとして扱う方法を考える必要がある。
ここで、始点から任意の広場まで移動した場合の楽しさを考えると、
(楽しさ) = (始点と任意の広場の標高差) - (余計なコスト)
と分解することができる。余計なコストを最小化することで楽しさを最大化できることがわかる。
余計なコストを最小化させる部分でダイクストラ法を使用することで、解を得ることができる。

## 計算量

ダイクストラ法：O(NlogM)
よって総計算量は
O(NlogM)

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

using P = pair<ll, int>;

const ll INF = 1LL << 60;

struct edge {
    int to, cost;
    edge(int to = 0, int cost = 0): to(to), cost(cost) {};
};
vector<vector<edge>> g;
vector<ll> dist;

void dijkstra(int s)
{
    // first : d, second : v
    priority_queue<P, vector<P>, greater<P>> q;
    dist[s] = 0;
    q.push({0, s});

    while (q.size()) {
        auto [d, v] = q.top(); q.pop();

        if (dist[v] != d) continue;
        for (auto e : g[v]) {
            auto t = e.to;
            auto c = e.cost;
            if (dist[t] <= dist[v] + c) continue;
            dist[t] = dist[v] + c;
            q.push({dist[t], t});
        }
    }
}

int main()
{
    int n, m;
    cin >> n >> m;

    vi h(n);
    rep(i, n) cin >> h[i];

    g.resize(n);
    dist.resize(n, INF);
    rep(i, m) {
        int u, v;
        cin >> u >> v;
        u--; v--;

        g[u].push_back(edge(v, max(0, h[v] - h[u])));
        g[v].push_back(edge(u, max(0, h[u] - h[v])));
    }

    dijkstra(0);

    ll ans = -INF;
    rep(i, n) chmax(ans, h[0] - h[i] - dist[i]);

    cout << ans << endl;

    return 0;
}
```
