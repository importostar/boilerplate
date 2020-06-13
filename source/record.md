---
title: record
date: 2020-05-07
---
Example Python program record.py

## Modules

* from collections import namedtuple

## Classes

* class Record:
* class M(Record):

## Methods

* def __init__(self, **kwargs):
* def __eq__(self, other):
* def __repr__(self):
* def test_repr():
* def test_eq():
* def test_not_eq():
* def test_not_eq_kind():
* def test_isinstance():
* def test_mutability():
* def test_attribute_error():

## Code

Python example

    class Record:
        __slots__ = ()
    
        def __init__(self, **kwargs):
            nonattrs = kwargs.keys() - set(self.__slots__)
            if nonattrs:
                raise ValueError(f'unexpected attributes: {nonattrs}')
            for a in self.__slots__:
                setattr(self, a, kwargs.get(a))
    
        def __eq__(self, other):
            return (
                hasattr(other, '__slots__') and
                self.__slots__ == other.__slots__ and
                all(getattr(self, a) == getattr(other, a) for a in self.__slots__)
            )
    
        def __repr__(self):
            items = [(a,getattr(self, a, None)) for a in self.__slots__]
            attrs = ', '.join(f'{a}={v}' for a,v in items)
            return f'{self.__class__.__name__}({attrs})'
    
    class M(Record):
        __slots__ = ('x', 'y')
    
    from collections import namedtuple
    P = namedtuple('P', 'x y')
    
    def test_repr():
        assert repr(P(1,1)) == 'P(x=1, y=1)'
        assert repr(M(x=1,y=1)) == 'M(x=1, y=1)'
    
    def test_eq():
        assert P(1, 1) == P(1, 1)
        assert M(x=1,y=1) == M(x=1,y=1)
    
    def test_not_eq():
        assert P(1, 1) != P(0, 0)
        assert M(x=1,y=1) != M(x=0,y=0)
    
    def test_not_eq_kind():
        assert P(1, 1) != None
        assert P(1, 1) != 'foo'
        assert M(x=1,y=1) != None
        assert M(x=1,y=1) != 'baz'
    
    def test_isinstance():
        assert isinstance(P(1, 1), P)
        assert isinstance(M(x=1,y=1), M)
    
    def test_mutability():
        m = M(x=1)
        assert m.x == 1
        m.x = 2
        assert m.x == 2
    
    def test_attribute_error():
        m = M()
        with pytest.raises(AttributeError):
            m.zzz = 'Yada'

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
