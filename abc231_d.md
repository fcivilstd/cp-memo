---
tags:
    - 無向グラフ
    - 閉路検出
---

# ABC231-D

[問題](https://atcoder.jp/contests/abc231/tasks/abc231_d)

## 考察

横一列に並べられない条件は、無向グラフで考えると

- 入次数が2より大きくなる頂点が存在する
- 閉路が存在する

の二つである。

無向グラフで閉路を検出するためには、同じ親を持つ頂点同士が連結すると閉路ができるという判定方法を使用すればよい。

## 計算量

入次数のカウント：O(M)
閉路の検出：O(Mα(N))

よって、総計算量は
O(Mα(N))

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

void no()
{
    cout << "No" << endl;
    exit(0);
}

int main()
{   
    int n, m;
    cin >> n >> m;

    UnionFind uf(n);
    vector<int> in(n);
    rep(i, m) {
        int a, b;
        cin >> a >> b;
        a--;b--;

        if (uf.same(a, b)) no();
        uf.unite(a, b);

        if (++in[a] > 2) no();
        if (++in[b] > 2) no();
    }

    cout << "Yes" << endl;

    return 0;
}
```
