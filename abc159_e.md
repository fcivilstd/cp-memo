---
tags:
    - 実装問
    - bit全探索
---

# abc159-E

[問題](https://atcoder.jp/contests/abc159/tasks/abc159_e)

## 考察

行の制約が小さいので、bit全探索して、グループ分けしながらホワイトチョコレートの個数を数えながら頑張って実装する。

## 計算量

bit全探索：O(2^H)
判定：O(W)
よって、総計算量は
O(W2^H)

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
    int h, w, k;
    cin >> h >> w >> k;

    vector<string> s(h);
    rep(i, h) cin >> s[i];

    int ans = INF;
    for (int bit = 0; bit < 1 << h - 1; bit++) {
        int gid = 0;
        vi group(h);
        // group id, count
        map<int, int> wht;
        rep(j, h - 1) {
            if (bit >> j & 1) group[j] = gid++;
            else group[j] = gid;
        }
        group[h - 1] = gid;

        int cnt = gid;

        rep(col, w) {
            bool flag = false;
            rep(row, h) {
                if (s[row][col] == '1') wht[group[row]]++;
            }
            rep(row, h) {
                for (auto [g, c] : wht) if (c > k) flag = true;
            }
            if (flag) {
                for (auto& [g, c] : wht) c = 0;
                cnt++;

                rep(row, h) {
                    if (s[row][col] == '1') wht[group[row]]++;
                }
                rep(row, h) {
                    if (s[row][col] == '1') {
                        if (wht[group[row]] > k) cnt = INF;
                    }
                }
            }

        }
        chmin(ans, cnt);
    }

    cout << ans << endl;

    return 0;
}
```
