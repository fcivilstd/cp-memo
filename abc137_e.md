---
tags:
    - ベルマンフォード法
    - グラフ理論
---

# ABC137-E

[問題](https://atcoder.jp/contests/abc137/tasks/abc137_e)

## 考察

まず、問題を考えやすくするために、一回の移動でP枚のコインを消費するとして各辺のコインの枚数からP枚を予め引いておく。また、コインの枚数の符号を逆にすることで、負辺を含む最短経路探索問題に帰着できる。
スコアが無限に大きくできる場合、負閉路が含まれることになる。負辺が含まれ、負閉路を検出できる必要がある最短経路探索問題は、ベルマンフォード法を使うとよい。

## 計算量

ベルマンフォード法：O(NM)
よって、総計算量は
O(MN)

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

struct edge
{
    int from, to, cost;
    edge(int from, int to, int cost): from(from), to(to), cost(cost) {}
};

const int inf = 1 << 30;

int main()
{
    int n, m, p;
    cin >> n >> m >> p;

    vector<edge> edges;
    vvi to(n), rto(n);
    rep(i, m) {
        int a, b, c;
        cin >> a >> b >> c;
        a--; b--;
        c -= p;
        edges.push_back(edge(a, b, -c));
        to[a].push_back(b);
        rto[b].push_back(a);
    }

    vi used(n);
    vi rused(n);

    auto bfs = [&](vi& _used, vvi& _to, int start){
        queue<int> q;
        q.push(start);
        _used[start]++;

        while (q.size()) {
            int v = q.front(); q.pop();
            for (auto t : _to[v]) {
                if (_used[t]) continue;
                q.push(t);
                _used[t]++;
            }
        }
    };

    bfs(used, to, 0);
    bfs(rused, rto, n - 1);

    vi ok(n);
    rep(i, n) ok[i] = used[i] & rused[i];

    vi dist(n, inf);
    dist[0] = 0;
    rep(cnt, n) {
        bool updated = false;
        rep(i, m) {
            int from, to, cost;
            from = edges[i].from;
            to = edges[i].to;
            cost = edges[i].cost;
            if (!ok[from] || !ok[to]) continue;
            if (chmin(dist[to], dist[from] + cost)) updated = true;
        }
        if (cnt == n - 1 && updated) {
            cout << -1 << endl;
            return 0;
        }
    }

    cout << max(-dist[n - 1], 0) << endl;

    return 0;
}
```
