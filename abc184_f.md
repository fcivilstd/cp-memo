---
tags:
    - 半分全列挙
    - bit全探索
---

# ABC184-F

[問題](https://atcoder.jp/contests/abc184/tasks/abc184_f)

## 考察

## 計算量

O(N(logN)2^(N/2))

## コーディング

丁寧な実装

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
    int n, t;
    cin >> n >> t;

    vi a, b;
    rep(i, n) {
        int ai;
        cin >> ai;
        if (i & 1) a.push_back(ai);
        else b.push_back(ai);
    }

    vector<ll> asum, bsum;
    for (int bit = 0; bit < 1 << a.size(); bit++) {
        ll tot = 0;
        rep(j, a.size()) {
            if ((bit >> j) & 1) tot += a[j];
        }
        asum.push_back(tot);
    }

    for (int bit = 0; bit < 1 << b.size(); bit++) {
        ll tot = 0;
        rep(j, b.size()) {
            if ((bit >> j) & 1) tot += b[j];
        }
        bsum.push_back(tot);
    }

    sort(all(bsum));

    ll ans = 0;
    rep(i, asum.size()) {
        if (t - asum[i] >= 0) {
            auto itr = upper_bound(all(bsum), t - asum[i]);
            itr--;
            chmax(ans, *itr + asum[i]);
        }
    }

    cout << ans << endl;

    return 0;
}
```

テクい実装

```cpp
#include<bits/stdc++.h>
#define rep(i, n) for (int i = 0; i < (int)(n); i++)
typedef long long ll;

using namespace std;

int main()
{
    int n, t;
    cin >> n >> t;

    vector<int> a(n);
    rep(i, n) cin >> a[i];

    vector<ll> b, c;
    b = c = {0};
    rep(i, n) {
        for (int j = b.size() - 1; j >= 0; j--) {
            b.push_back(b[j] + a[i]);
        }
        swap(b, c);
    }

    sort(b.begin(), b.end());

    ll ans = 0;
    for (ll s : c) {
        if (s > t) continue;
        s += *prev(upper_bound(b.begin(), b.end(), t - s));
        ans = max(ans, s);
    }

    cout << ans << endl;

    return 0;
}
```
