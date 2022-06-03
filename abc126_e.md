---
tags:
    - Union-Find
    - 連結グラフ
---

# ABC125-E

[問題](https://atcoder.jp/contests/abc126/tasks/abc126_e)

## 考察

x、 yが与えられた場合、どちらかが分かればもう一方も分かる。したがって、x、yを辺で繋げた無向グラフが連結グラフであれば、その中の一つでも分かれば他すべてが分かる。連結グラフの数が解となる。

## 計算量

Union-Findでの連結判定：O(α(M))
よって、総計算量は
O(Nα(M))

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

int main()
{
    int n, m;
    cin >> n >> m;

    UnionFind uf(n);
    rep(i, m) {
        int x, y, z;
        cin >> x >> y >> z;
        x--; y--;

        uf.unite(x, y);
    }

    int ans = 0;
    rep(i, n) if (uf.find(i) == i) ans++;

    cout << ans << endl;

    return 0;
}
```
