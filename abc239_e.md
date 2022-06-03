---
tags:
    - グラフ理論
    - 木
    - 部分木
    - vectorの連結
---

# ABC239-E

[問題](https://atcoder.jp/contests/abc239/tasks/abc239_e)

## 考察

部分木について考える場合は、DFSで下から見ていくのが定石。部分木のマージは、vectorを連結できるメソッドであるinsertを使用するとよい。

## 計算量

ソート：O(NKlog(NK))
よって、総計算量は
O(NKlog(NK))

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

const int K = 20;
int n, q;
vector<int> x;
vector<vector<int>> to;
vector<pair<int, int>> vk;
map<int, vector<int>> mvk;
map<pair<int, int>, int> ans;

void merge(vector<int>& a, const vector<int> b)
{
    a.insert(a.end(), b.begin(), b.end());
    sort(a.rbegin(), a.rend());
    a.resize(K);
}

vector<int> dfs(int v, int p)
{
    vector<int> elm;
    elm.push_back(x[v]);
    for (auto t : to[v]) {
        if (t == p) continue;
        merge(elm, dfs(t, v));
    }

    for (auto k : mvk[v]) {
        ans[make_pair(v, k)] = elm[k - 1];
    }

    return elm;
}

int main()
{
    cin >> n >> q;

    x.resize(n);
    rep(i, n) cin >> x[i];

    to.resize(n);
    rep(i, n - 1) {
        int a, b;
        cin >> a >> b;
        a--; b--;
        to[a].push_back(b);
        to[b].push_back(a);
    }

    vk.resize(q);
    rep(i, q) {
        int v, k;
        cin >> v >> k;
        v--;
        vk[i].first = v;
        vk[i].second = k;
        mvk[v].push_back(k);
    }

    dfs(0, -1);

    rep(i, q) {
        auto [a, b] = vk[i];
        cout << ans[make_pair(a, b)] << endl;
    }

    return 0;
}
```
