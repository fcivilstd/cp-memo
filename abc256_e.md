---
tags:
    - 最小全域木
    - クラスカル法
    - Union-Find
    - SCC
---

# ABC256-E

[問題](https://atcoder.jp/contests/abc256/tasks/abc256_e)

## 考察

閉路の中で最も不満度の低い辺を除去すれば良いため、最小全域木で解くことができる。
また、強連結成分分解をして閉路を抽出して、そこから最も不満度が小さいものを選ぶ方法でも解くことができる。

## 計算量

クラスカル法：O(NlogN)
よって、総計算量は
O(NlogN)

## コーディング

クラスカル法

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

struct UnionFind {
    // root node: -1 * size
    // otherwise: parent
    vector<int> parent_or_size;

    UnionFind() {}
    UnionFind(int n)
    {
        parent_or_size.resize(n, -1);
    }

    void unite(int x, int y)
    {
        int xp = find(x);
        int yp = find(y);
        if (xp == yp) return;
        if (-1 * parent_or_size.at(xp) < -1 * parent_or_size.at(yp)) swap(xp, yp);
        parent_or_size.at(xp) += parent_or_size.at(yp);
        parent_or_size[yp] = xp;
    }

    // find parent
    int find(int x)
    {
        if (parent_or_size.at(x) < 0) return x;
        return parent_or_size.at(x) = find(parent_or_size.at(x));
    }

    bool same(int x, int y)
    {
        return find(x) == find(y);
    }

    int size(int x)
    {
        return -1 * parent_or_size.at(find(x));
    }
};

struct Edge
{
    int a, b, cost;
    Edge(int a = 0, int b = 0, int cost = 0): a(a), b(b), cost(cost) {};

    bool operator<(const Edge& o) const {
        return cost < o.cost;
    }
};

int main()
{
    int n;
    cin >> n;

    vi x(n), c(n);
    rep(i, n) cin >> x[i];
    rep(i, n) x[i]--;
    rep(i, n) cin >> c[i];

    vector<Edge> es;
    rep(i, n) {
        es.push_back(Edge(i, x[i], -c[i]));
    }

    sort(all(es));

    ll ans = 0;
    UnionFind uf(n);
    rep(i, n) {
        Edge& e = es[i];
        if (!uf.same(e.a, e.b)) {
            uf.unite(e.a, e.b);
        } else {
            ans += -e.cost;
        }
    }

    cout << ans << endl;

    return 0;
}
```

SCC

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

vi visited;
vvi to, rto;
vi ord;
vvi groups;

void dfs(int v)
{
    visited[v] = 1;
    for (auto t : to[v]) {
        if (visited[t]) continue;
        dfs(t);
    }
    ord.push_back(v);
}

void rdfs(int v)
{
    visited[v] = 1;
    groups.back().push_back(v);
    for (auto t : rto[v]) {
        if (visited[t]) continue;
        rdfs(t);
    }
}

int main()
{
    int n;
    cin >> n;

    vi x(n), c(n);
    rep(i, n) cin >> x[i];
    rep(i, n) x[i]--;
    rep(i, n) cin >> c[i];

    visited.resize(n);
    to.resize(n);
    rto.resize(n);

    rep(i, n) {
        to[i].push_back(x[i]);
        rto[x[i]].push_back(i);
    }

    rep(i, n) {
        if (visited[i]) continue;
        dfs(i);
    }

    rep(i, n) visited[i] = 0;
    reverse(all(ord));

    for (auto v : ord) {
        if (visited[v]) continue;
        groups.push_back(vi(0));
        rdfs(v);
    }

    ll ans = 0;
    for (auto g : groups) {
        if (g.size() == 1) continue;

        int cost = 1001001001;
        for (auto v : g) {
            chmin(cost, c[v]);
        }
        ans += cost;
    }

    cout << ans << endl;

    return 0;
}
```
