---
tags:
    - グラフ理論
    - 二部グラフ判定
---

# Codeforces Round #805-E

[問題](https://codeforces.com/contest/1702/problem/E)

## 考察

満たすべき条件は、

- 1からNまでがちょうど2回出てくる
- 表裏が同じ数字でない
- 二部グラフである

## 計算量

二部グラフ判定：O(N)
よって、総計算量は
O(N)

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

int main()
{
    int t;
    cin >> t;

    while (t--) {
        int n;
        cin >> n;

        bool ans = true;
        vvi to(n);
        rep(i, n) {
            int a, b;
            cin >> a >> b;
            a--; b--;
            to[a].push_back(b);
            to[b].push_back(a);
            if (a == b || to[a].size() > 2 || to[b].size() > 2) ans = false;
        }

        auto f = [&](){
            // v, color
            queue<pii> q;
            vi visited(n);
            vi color(n);

            rep(i, n) {
                if (visited[i]) continue;

                q.push({i, -1});
                visited[i]++;
                color[i] = -1;

                while (q.size()) {
                    auto [v, c] = q.front(); q.pop();
                    for (auto t : to[v]) {
                        if (color[t] == c) return false;
                        if (visited[t]) continue;
                        q.push({t, -c});
                        visited[t]++;
                        color[t] = -c;
                    }
                }
            }

            return true;
        };

        if (!f()) ans = false;

        if (ans) cout << "YES" << endl;
        else cout << "NO" << endl;
    }

    return 0;
}
```
