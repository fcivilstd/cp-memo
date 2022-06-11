---
tags:
    - グラフ理論
    - 状態をBFS
---

# ABC224-D

[問題](https://atcoder.jp/contests/abc224/tasks/abc224_d)

## 考察

パズルの配置の状態をそのままキーにしてBFSで最小化すればよい。

## 計算量

???

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
    int m;
    cin >> m;

    vvi to(9);
    rep(i, m) {
        int u, v;
        cin >> u >> v;
        u--; v--;

        to[u].push_back(v);
        to[v].push_back(u);
    }

    vi p(9, -1);
    rep(i, 8) {
        int pi;
        cin >> pi;
        pi--;
        p[pi] = i;
    }

    map<vi, int> dist;
    auto _p = p;
    sort(all(_p));
    do dist[_p] = INF;
    while (next_permutation(all(_p)));

    queue<vi> q;
    q.push(p);
    dist[p] = 0;

    while (q.size()) {
        auto now = q.front(); q.pop();
        rep(i, 9) for (auto t : to[i]) {
            if (now[t] != -1) continue;
            auto nxt = now;
            swap(nxt[i], nxt[t]);
            if (chmin(dist[nxt], dist[now] + 1)) q.push(nxt);
            break;
        }
    }

    vi end(9, -1);
    rep(i, 8) end[i] = i;
    if (dist[end] != INF) cout << dist[end] << endl;
    else cout << -1 << endl;

    return 0;
}
```
