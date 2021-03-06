---
title: pycombinator
date: 2020-05-07
---
Example Python program pycombinator.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import re

## Classes

* class ParseResult:
* class ParseSuccess(ParseResult):
* class ParseFailure(ParseResult):
* class Parser:
* class RepeatParser(Parser):
* class RegexParser(Parser):
* class FlatMapParser(Parser):
* class MapParser(Parser):
* class OrParser(Parser):
* class CatParser(Parser):
* class StringParser(Parser):
* class DelayedParser(Parser):

## Methods

* def __init__(self, next):
* def success(self):
* def __init__(self, value, next):
* def success(self):
* def __init__(self, next):
* def success(self):
* def parse(self, input):
* def mor(self, rhs):
* def cat(self, rhs):
* def map(self, fun):
* def flat_map(self, fun):
* def rep(self):
* def chainlI(self, p, q):
* def fun(value):
* def chainl(self, q):
* def __init__(self, parser):
* def parse(self, input):
* def __init__(self, regex_string):
* def parse(self, input):
* def __init__(self, parser, fun):
* def parse(self, input):
* def __init__(self, parser, fun):
* def parse(self, input):
* def __init__(self, lhs, rhs):
* def parse(self, input):
* def __init__(self, lhs, rhs):
* def parse(self, input):
* def __init__(self, literal):
* def parse(self, input):
* def __init__(self, fun):
* def parse(self, input):
* def s(literal):
* def reg(regex_string):
* def f(fun):
* def rule(fun):
* def chainl(p, q):

## Code

Python example

    import re
    
    class ParseResult:
        def __init__(self, next):
            self.next = next
    
        def success(self):
            pass
    
    class ParseSuccess(ParseResult):
        def __init__(self, value, next):
            super(ParseSuccess, self).__init__(next)
            self.value = value
    
        @property
        def success(self):
            return True
    
    class ParseFailure(ParseResult):
        def __init__(self, next):
            super(ParseFailure, self).__init__(next)
    
        @property
        def success(self):
            return False
    
    class Parser:
        def parse(self, input):
            return ParseFailure(input)
    
        def mor(self, rhs):
            return OrParser(self,  rhs)
    
        def cat(self, rhs):
            return CatParser(self, rhs)
    
        def map(self, fun):
            return MapParser(self, fun)
    
        def flat_map(self, fun):
            return FlatMapParser(self, fun)
    
        def rep(self):
            return RepeatParser(self)
    
        def chainlI(self, p, q):
            def fun(value):
                x = value[0]
                xs = value[1]
                a = x
                while len(xs)> 0:
                    f = xs[0][0]
                    b = xs[0][1]
                    a = f(a, b)
                    del xs[0]
                return a
            value = self.cat((q.cat(p).rep())).map(fun)
            return value
    
        def chainl(self, q):
            return self.chainlI(self, q)
    
    class RepeatParser(Parser):
        def __init__(self, parser):
            super(RepeatParser, self).__init__()
            self.parser = parser
    
        def parse(self, input):
            rest = input
            values = []
            while True:
                r = self.parser.parse(rest)
                if not r.success: return ParseSuccess(values, rest)
                values.append(r.value)
                rest = r.next
            pass
    
    
    class RegexParser(Parser):
        def __init__(self, regex_string):
            super(RegexParser, self).__init__()
            self.pattern = re.compile(regex_string)
    
        def parse(self, input):
            m = self.pattern.match(input)
            if m != None:
                s, e = m.span()
                return ParseSuccess(input[s:e], input[e:])
            else:
                return ParseFailure(input)
    
    class FlatMapParser(Parser):
        def __init__(self, parser, fun):
            super(FlatMapParser, self).__init__()
            self.parser = parser
            self.fun = fun
    
        def parse(self, input):
            r = self.parser.parse(input)
            if not r.success: return r
            return self.fun(r.value).parse(r.next)
    
    class MapParser(Parser):
        def __init__(self, parser, fun):
            super(MapParser, self).__init__()
            self.parser = parser
            self.fun = fun
    
        def parse(self, input):
            r = self.parser.parse(input)
            if not r.success: return r
            return ParseSuccess(self.fun(r.value), r.next)
    
    class OrParser(Parser):
        def __init__(self, lhs, rhs):
            super(OrParser, self).__init__()
            self.lhs = lhs
            self.rhs = rhs
    
        def parse(self, input):
            r = self.lhs.parse(input)
            if r.success:
                return r
            else:
                return self.rhs.parse(input)
    
    
    class CatParser(Parser):
        def __init__(self, lhs, rhs):
            super(CatParser, self).__init__()
            self.lhs = lhs
            self.rhs = rhs
    
        def parse(self, input):
            r1 = self.lhs.parse(input)
            if r1.success:
                r2 = self.rhs.parse(r1.next)
                if r2.success:
                    return ParseSuccess([r1.value, r2.value], r2.next)
                else:
                    return ParseFailure(r1.next)
            else:
                return ParseFailure(input)
    
    class StringParser(Parser):
        def __init__(self, literal):
            super(StringParser, self).__init__()
            self.literal = literal
    
        def parse(self, input):
            if input.startswith(self.literal):
                rest = input[len(self.literal):]
                return ParseSuccess(self.literal, rest)
            else:
                return ParseFailure(input)
    
    class DelayedParser(Parser):
        def __init__(self, fun):
            super(DelayedParser, self).__init__()
            self.fun = fun
    
        def parse(self, input):
            return self.fun().parse(input)
    
    def s(literal):
        return StringParser(literal)
    
    def reg(regex_string):
        return RegexParser(regex_string)
    
    def f(fun):
        return DelayedParser(fun)
    
    def rule(fun):
        return DelayedParser(fun)
    
    def chainl(p, q):
        return p.chainl(q)
    
    E = rule(lambda : A)
    A = rule((lambda :
            M.chainl(
                (
                    s('+').map(lambda op: (lambda lhs, rhs: lhs + rhs))
                ).mor(
                    s('-').map(lambda op: (lambda lhs, rhs: lhs - rhs))
                )
            )))
    M = rule((lambda :
            P.chainl(
                (
                    s('*').map(lambda op: (lambda lhs, rhs: lhs * rhs))
                ).mor(
                    s('/').map(lambda op: (lambda lhs, rhs: lhs / rhs))
                )
            )))
    P = rule((lambda :
            (s('(').cat(E)).cat(s(')')).map(lambda values: values[0][1]).mor(N)
            ))
    
    N = rule((lambda :
            reg('[0-9]+').map(lambda n: int(n))))
    
    
    r = int(E.parse("111+222").value)
    print(r)
    r = int(E.parse("(1+2*3)*4").value)
    print(r)
    r = int(E.parse("(3+2*4)/3").value)
    print(r)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
