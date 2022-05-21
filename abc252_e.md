---
tags:
    - ダイクストラ法
    - 経路復元
---

# ABC252-E

[問題](https://atcoder.jp/contests/abc252/tasks/abc252_e)

## 考察

ダイクストラ法で確定した経路を残せばよい。経路復元では、ある頂点へ到達するための最後に更新された辺が保存されていればよい。

## 計算量

ダイクストラ法：O(MlogN)

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

typedef pair<ll, int> P;

struct edge {
    int to, cost, id;
    edge(int to = 0, int cost = 0, int id = 0): to(to), cost(cost), id(id) {};
};
vector<vector<edge>> g;
vector<ll> dist;
vector<int> ans;

void dijkstra(int s)
{
    // first : d, second : v
    priority_queue<P, vector<P>, greater<P>> q;
    dist[s] = 0;
    q.push({0, s});

    while (q.size()) {
        auto p = q.top(); q.pop();
        auto d = p.first;
        auto v = p.second;

        if (dist[v] != d) continue;
        for (auto e : g[v]) {
            auto t = e.to;
            auto c = e.cost;
            auto id = e.id;
            if (dist[t] <= dist[v] + c) continue;
            dist[t] = dist[v] + c;
            q.push({dist[t], t});
            ans[t] = id;
        }
    }
}

int main()
{
    int n, m;
    cin >> n >> m;

    g.resize(n);
    dist.resize(n, 1LL << 60);
    ans.resize(n);
    rep(i, m) {
        int a, b, c;
        cin >> a >> b >> c;
        a--; b--;
        edge e1(a, c, i + 1), e2(b, c, i + 1);
        g[a].push_back(e2);
        g[b].push_back(e1);
    }

    dijkstra(0);

    rng(i, 1, n) cout << ans[i] << " \n"[i == n - 1];

    return 0;
}
```
