---
tags:
    - 遅延セグメント木
    - RSQ
    - RAQ
    - 区間和取得
    - 区間加算
---

# AOJ-RSQ and RAQ

[問題](https://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=DSL_2_G&lang=ja)

## 考察

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

struct D
{
    ll value;
    int size;
};

template <class S, class F>
struct LazySegTree {
    // edit ↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓

    // 区間取得の演算
    S op(S a, S b)
    {
        return {a.value + b.value, a.size + b.size};
    }

    // 単位元
    // op(a, e) = a
    S e()
    {
        return {0, 0};
    }

    // lazy(f) -> data(x)
    S mapping(F f, S x)
    {
        return {x.value + f * x.size, x.size};;
    }

    // lazy(f) -> lazy(g)
    F composition(F f, F g)
    {
        return f + g;
    }

    // 恒等写像
    // mapping(id, a) = a
    F id()
    {
        return 0;
    }

    // edit ↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑↑

    int _n, _size, _depth;
    // _data[1] ~ _data[_size + _n - 1]
    // 与えられた配列 _data[_size] ~ _data[_size + _n - 1]
    vector<S> _data;
    // _lazy[1] ~ _lazy[_size + _n - 1]
    vector<F> _lazy;

    LazySegTree() : LazySegTree(0) {}
    LazySegTree(int n) : LazySegTree(vector<S>(n, e())) {}
    LazySegTree(const vector<S>& v) : _n(int(v.size())) {
        _size = 1;
        _depth = 0;
        while (_size < _n) {
            _size <<= 1;
            _depth++;
        }

        _data = vector<S>(2 * _size, e());
        _lazy = vector<F>(2 * _size, id());

        for (int i = 0; i < _n; i++) _data[_size + i] = v[i];
        for (int i = _size - 1; i >= 1; i--) update(i);
    }

    void update(int k)
    {
        _data[k] = op(_data[2 * k], _data[2 * k + 1]);
    }

    // _lazyを伝搬
    // _dataの更新
    void push(int k)
    {
        if (k < _size) {
            _lazy[2 * k] = composition(_lazy[k], _lazy[2 * k]);
            _lazy[2 * k + 1] = composition(_lazy[k], _lazy[2 * k + 1]);
        }

        _data[k] = mapping(_lazy[k], _data[k]);
        _lazy[k] = id();
    }

    S prod(int a, int b, int k, int l, int r)
    {
        push(k);
        if (l == r) return e();
        if (r <= a || b <= l) return e();
        if (a <= l && r <= b) return _data[k];

        S lv = prod(a, b, 2 * k, l, (l + r) >> 1);
        S rv = prod(a, b, 2 * k + 1, (l + r) >> 1, r);

        return op(lv, rv);
    }

    void update(int a, int b, F f, int k, int l, int r)
    {
        push(k);
        if (r <= a || b <= l) return;
        if (a <= l && r <= b) {
            _lazy[k] = composition(f, _lazy[k]);
            push(k);
        } else {
            update(a, b, f, 2 * k, l, (l + r) >> 1);
            update(a, b, f, 2 * k + 1, (l + r) >> 1, r);

            update(k);
        }
    }

    // 値の取得
    S get(int k)
    {
        k += _size;
        for (int i = _depth; i >= 0; i--) push(k >> i);
        return _data[k];
    }

    // 区間取得
    // 0-indexed
    // [l, r)
    S prod(int l, int r)
    {
        return prod(l, r, 1, 0, _size);
    }

    // 一点更新(上書き)
    void set(int k, S x)
    {
        k += _size;
        for (int i = _depth; i >= 0; i--) push(k >> i);
        _data[k] = x;
        for (int i = 1; i <= _depth; i++) update(k >> i);
    }

    // 一点更新
    void update(int k, F f)
    {
        update(k, k + 1, f);
    }

    // 区間更新
    // 0-indexed
    // [l, r)
    void update(int l, int r, F f)
    {
        update(l, r, f, 1, 0, _size);
    }
};

int main()
{
    int n, q;
    cin >> n >> q;

    vector<D> v(n, {0, 1});
    LazySegTree<D, ll> seg(v);

    while (q--) {
        int t;
        cin >> t;

        if (t == 0) {
            int s, t, x;
            cin >> s >> t >> x;
            s--; t--;

            seg.update(s, t + 1, x);
        } else {
            int s, t;
            cin >> s >> t;
            s--; t--;

            cout << seg.prod(s, t + 1).value << endl;
        }
    }

    return 0;
}
```
