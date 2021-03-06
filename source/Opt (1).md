---
title: Opt (1)
date: 2020-05-07
---
Example Python program Opt (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys

## Classes

* class SearchYforFXY:
* class SearchXforFXY:

## Methods

* def Const(x):
* def Merge3(n,x,y):
* def __init__(self, f, x, yy, q):
* def __call__(self, u):
* def __init__(self, f, xx, yy, q):
* def __call__(self, u):
* def lift4(f, xx, yy, q):
* def after3(tt, m, q):
* def between4(tt, m, p, q):
* def arbitrary(x):
* def limit(f):
* def raw(p):
* def partial(n):
* def ff(p):
* def cook(t):
* def weights(w, acc, r):
* def split(p, v, r):
* def optimize(r):

## Code

Python example

    #!/usr/bin/python3
    
    import sys
    sys.setrecursionlimit(1000000)
    
    def Const(x):
        return lambda y, x=x: x
    
    def Merge3(n,x,y):
        return lambda u, n=n, x=x, y=y: x(u) if u < n else y(u)
    
    class SearchYforFXY:
        __slots__ = 'f', 'x', 'yy', 'q', 'y'
        def __init__(self, f, x, yy, q):
            self.f = f
            self.x = x
            self.yy = yy
            self.q = q
            self.y = None
        def __call__(self, u):
            if self.y is None:
                self.y = self.yy(
                    lambda y, q=self.q, f=self.f, x=self.x: q(Merge3(f,x,y)))
            return self.y(u)
    
    class SearchXforFXY:
        __slots__ = 'f', 'xx', 'yy', 'q', 'x'
        def __init__(self, f, xx, yy, q):
            self.f = f
            self.xx = xx
            self.yy = yy
            self.q = q
            self.x = None
    
        def __call__(self, u):
            if self.x is None:
                self.x = self.xx(
                    lambda x, f=self.f, yy=self.yy, q=self.q: q(
                        Merge3(f, x, SearchYforFXY(f, x, yy, q))))
            return self.x(u)
    
    def lift4(f, xx, yy, q):
        x = SearchXforFXY(f, xx, yy, q)
        y = SearchYforFXY(f, x, yy, q)
        return Merge3(f, x, y)
    
    def after3(tt, m, q):
        n = 2 * m + 1
        return lift4(n,
                     lambda q, tt=tt, m=m, n=n: between4(tt, m, n, q),
                     lambda q, tt=tt, n=n: after3(tt, n, q),
                     q)
    
    def between4(tt, m, p, q):
        if m + 1 == p:
            return lambda _, x=q(tt): x
        n = (m + p) // 2
        return lift4(n,
                     lambda q, tt=tt, m=m, n=n: between4(tt, m, n, q),
                     lambda q, tt=tt, n=n, p=p: between4(tt, n, p, q),
                     q)
    
    def arbitrary(x):
        return False
    
    def limit(f):
        m = 0
        n = 1
        while not f(n):
            m = n
            n = 2 * m + 1
        while m + 1 < n:
            p = (m + n) // 2
            if f(p):
                n = p
            else:
                m = p
        return m
    
    def raw(p):
        something = p(arbitrary)
        different = after3(Const(not something), 0, p)
        if p(different) == something:
            return not not something
        def partial(n):
            return p(Merge3(n, different, arbitrary)) != something
        pivot = limit(partial)
        rawT = raw(lambda f: p(lambda x: x == pivot or  f(x)))
        rawF = raw(lambda f: p(lambda x: x != pivot and f(x)))
        return pivot, rawT, rawF
    
    def ff(p):
        n = 0
        if p(111111111111111):
            n += 1
        if p(222222222222222):
            n += 2
        if p(333333333333333):
            n += 4
        return p(n) != p(n+1)
    
    def cook(t):
        if type(t) is bool:
            return t
        pp, tt, ff = t
        if tt is True:
            if ff is False:
                return f'@{pp}'
            return f'@{pp}|', cook(ff)
        if tt is False:
            if ff is True:
                return f'!{pp}'
            return f'!{pp}&', cook(ff)
        if ff is True:
            return f'!{pp}|', cook(tt)
        if ff is False:
            return f'@{pp}&', cook(tt)
        return pp, cook(tt), cook(ff)
    
    golden = 0.61803398875
    
    def weights(w, acc, r):
        if type(r) is bool:
            return
        pp, tt, ff = r
        acc[pp] = w + acc.get(pp, 0)
        w *= golden
        weights(w, acc, tt)
        weights(w, acc, ff)
    
    def split(p, v, r):
        if type(r) is bool:
            return r
        pp, tt, ff = r
        if pp == p:
            return tt if v else ff
        tt = split(p, v, tt)
        ff = split(p, v, ff)
        if tt == ff:
            return tt
        else:
            return pp, tt, ff
    
    def optimize(r):
        if type(r) is bool:
            return r
        pp, tt, ff = r
        if type(tt) is bool or type(ff) is bool:
            return r
        w = {}
        weights(1, w, r)
        p = max(w.items(), key=lambda x: x[1])[0]
        stt = optimize(split(p, True, r))
        sff = optimize(split(p, False, r))
        if stt == sff:
            return stt
        else:
            return p, stt, sff
    
    if __name__ == "__main__":
        r = raw(ff)
        print(r)
        print()
        print(cook(r))
        print()
        print(cook(optimize(r)))
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
