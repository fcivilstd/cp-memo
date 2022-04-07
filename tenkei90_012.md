---
tags:
    - Union-Find
---

# 典型90-012

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_l)

## 考察

愚直に考えると、グリッド上を走査することで解が得られるが、最悪ケースで計算量がO(QHW)となるため、この問題の制約では厳しい。
連結判定はUnion-Findを用いることで効率的に行うことができる。

## 計算量

Union-Find木の構築：O(HW)
Union-Findでの連結判定：O(α(HW))
クエリの受け取り：O(Q)
よって、総計算量は
O(HW + Qα(HW))

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

int main()
{
    int h, w, q;
    cin >> h >> w >> q;

    auto f = [&](int x, int y) {
        return w * x + y;
    };

    int dx[] = {0, 1, 0, -1};
    int dy[] = {1, 0, -1, 0};
    vector<vector<int>> grid(h, vector<int>(w));
    UnionFind uf(h * w);
    rep(i, q) {
        int qi;
        cin >> qi;

        if (qi == 1) {
            int r, c;
            cin >> r >> c;
            r--; c--;
            grid[r][c] = 1;
            rep(j, 4) {
                int tr = r + dx[j];
                int tc = c + dy[j];
                if (tr < 0 || tr >= h || tc < 0 || tc >= w) continue;
                if (grid[tr][tc]) {
                    uf.unite(f(r, c), f(tr, tc));
                }
            }
        } else {
            int ra, ca, rb, cb;
            cin >> ra >> ca >> rb >> cb;
            ra--; ca--; rb--; cb--;
            if (uf.same(f(ra, ca), f(rb, cb)) && grid[ra][ca] && grid[rb][cb]) cout << "Yes" << endl;
            else cout << "No" << endl;
        }
    }

    return 0;
}
```
