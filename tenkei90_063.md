---
tags:
    - 全探索
    - bit全探索
---

# 典型90-063

[問題](https://atcoder.jp/contests/typical90/tasks/typical90_bk)

## 考察

制約を見ると、Hが小さいため、行を全探索すれば良いことに気づく。

## 計算量

行のbit全探索：O(2^H)
列の探索：O(W)
よって、総計算量は
O(2^H * W)

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

int main()
{
    int h, w;
    cin >> h >> w;

    vector<vector<int>> p(h, vector<int>(w));
    rep(i, h) rep(j, w) cin >> p[i][j];

    int ans = 0;
    for (int bit = 1; bit < 1 << h; bit++) {
        vector<int> row;
        rep(i, h) {
            if (bit >> i & 1) row.push_back(i);
        }

        map<int, int> mp;
        rep(i, w) {
            bool flag = true;
            int t = p[row.front()][i];
            for (auto r : row) {
                if (t != p[r][i]) {
                    flag = false;
                    break;
                }
                t = p[r][i];
            }
            if (flag) mp[t]++;
        }
        
        for (auto [key, val] : mp) chmax(ans, row.size() * val);
    }

    cout << ans << endl;

    return 0;
}
```
