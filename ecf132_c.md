---
tags:
    - 正しい括弧列
    - 貪欲法
---

# Educatinal Codeforces Round #132-C

[問題](https://codeforces.com/contest/1709/problem/C)

## 考察

まず正しい括弧列の条件とは、

- '('を+1')'を-1としたときに累積和が最終的に0
- 累積和の最小値が0

である。
このことから、'?'に'('または')'を割り当てていくことを考えるとき、最終的に0になるのであれば、できるだけ'('を先に割り当てる方が正しい括弧列である可能性は高くなる。また、割り当ての方法がユニークであるとき、'('を割り当てるより先に絶対に')'を割り当てられないことから、最後の'('の割り当てと、最初の')'の割り当てを入れ替えて正しい括弧列であればユニークでないと判定することができる。

## 計算量

O(|S|)

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

bool isRBS(string& s)
{
    int mn = 1 << 30;
    int psum = 0;
    rep(i, s.size()) {
        if (s[i] == '(') {
            psum++;
        } else {
            psum--;
        }
        chmin(mn, psum);
    }

    if (mn >= 0 && psum == 0) return true;
    else return false;
}

int main()
{
    int t;
    cin >> t;

    while (t--) {
        string s;
        cin >> s;

        vi qpos;
        int psum = 0, qcnt = 0;

        rep(i, s.size()) {
            int dlt = 0;
            if (s[i] == '?') {
                qcnt++;
                qpos.push_back(i);
            } else if (s[i] == '(') {
                dlt++;
            } else {
                dlt--;
            }
            psum += dlt;
        }

        auto unq = [&](){
            int open = (-psum + qcnt) / 2, _open = open;
            if (open == 0 || open == qcnt) return true;

            rep(i, s.size()) {
                int dlt = 0;
                if (s[i] == '?') {
                    if (_open) s[i] = '(', _open--;
                    else s[i] = ')';
                }
            }

            s[qpos[open - 1]] = ')';
            s[qpos[open]] = '(';
            return !isRBS(s);
        };

        if (unq()) cout << "YES" << endl;
        else cout << "NO" << endl;
    }

    return 0;
}
```
