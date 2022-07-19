---
tags:
    - グリッドの90°回転
---

# Codeforces Round #806-E

[問題](https://codeforces.com/contest/1703/problem/E)

## 考察

グリッドを90°回転させると、移動後のインデックスは
(x, y) -> (tx, ty)
ただし、
tx = y
ty = n - 1 - x

## 計算量

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

int cnt[100][100][2];
int checked[100][100];

int main()
{
    int t;
    cin >> t;

    while (t--) {
        int n;
        cin >> n;

        vector<string> g(n);
        rep(i, n) cin >> g[i];

        rep(i, n) rep(j, n) rep(k, 2) cnt[i][j][k] = 0;
        rep(i, n) rep(j, n) checked[i][j] = 0;

        int ans = 0;
        rep(i, n) rep(j, n) if (!checked[i][j]) {
            int cnt0 = 0, cnt1 = 0;
            int x = i, y = j;
            rep(r, 4) {
                if (g[x][y] == '0') cnt0++;
                else cnt1++;

                checked[x][y]++;
                int tx = y, ty = n - 1 - x;
                x = tx, y = ty;
            }
            ans += min(cnt0, cnt1);
        }

        cout << ans << endl;
    }

    return 0;
}
```

ライブラリ

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

vector<string> grid_r90(vector<string> &grid)
{
    int _h = grid.size(), _w = grid[0].size();
    vector<string> ret(_w, string(_h, '.'));
    rep(i, _h) rep(j, _w) ret[_w - 1 - j][i] = grid[i][j];
    return ret;
}

int main()
{
    int t;
    cin >> t;

    while (t--) {
        int n;
        cin >> n;

        vector<string> g(n);
        rep(i, n) cin >> g[i];

        int cnt[100][100][2];
        rep(i, 100) rep(j, 100) rep(k, 2) cnt[i][j][k] = 0;

        int times = 4;
        while (times--) {
            rep(i, n) rep(j, n) {
                if (g[i][j] == '1') cnt[i][j][1]++;
                else cnt[i][j][0]++;
            }

            g = grid_r90(g);
        }

        int ans = 0;
        rep(i, n) rep(j, n) {
            if (!cnt[i][j][0] || !cnt[i][j][1]) continue;
            ans += min(cnt[i][j][0], cnt[i][j][1]);
        }

        cout << ans / 4 << endl;
    }

    return 0;
}
```
