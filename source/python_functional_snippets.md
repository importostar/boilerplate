---
title: python_functional_snippets
date: 2020-05-07
---
Example Python program python_functional_snippets.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* # from toolz.functoolz import curry,partial,compose,flip,pipe as datapipe
* from functools import reduce
* from functools import partial

## Methods

* def cond(predicateFnMatrix):
*   def condInner(*args):
* def logFn(fn,name=""):
* def fn_logger(*args,**kwargs):
* def len_minus1(collection): return len(collection) - 1
* def pipe(firstFn, *fns): 
* def pipeInner(lastArg,*args):
* def to_transformer(fn,acc):
*   def inner(acc,v,k,c):
* def curry(fn,arity=2):
*   def curryInner(*args,**kwargs):
* def assign_dicts(dest,*dicts):
* def assign_dicts(dest,*dicts):
* def analyze_graph(get_adjacent_vertices,collection}):

## Code

Python example

    # from toolz.functoolz import curry,partial,compose,flip,pipe as datapipe
    
    
    #logic
    def cond(predicateFnMatrix):
      def condInner(*args):
        for (predicate,fn) in predicateFnMatrix:
          if predicate(*args):
            return fn(*args)
      return condInner
    all = lambda *fns: lambda *args,**kwargs: reduce((lambda truth,fn:(fn(*args,**kwargs) if truth else truth)),fns,True)
    ifElse = lambda predicate,fnTrue,fnFalse: lambda *a,**kw: fnTrue(*a,**kw) if predicate(*a,**kw) else fnFalse(*a,**kw)
    
    
    # predicates
    lt = curry(lambda x,y: y < x)
    lte = curry(lambda x,y: y <= x)
    gt = curry(lambda x,y: y > x)
    gte = curry(lambda x,y: y >= x)
    eq = curry(lambda x,y: y == x)
    ne = curry(lambda x,y: y != x)
    is_ = curry(lambda x,y: x is y)
    is_not = curry(lambda x,y: x is not y)
    
    #debugging
    plog = lambda *args: print(*args) or args[0]
    def logFn(fn,name=""):
        def fn_logger(*args,**kwargs):
            print(name,'args:',args,'kwargs:',kwargs)
            return fn(*args,**kwargs)
        return fn_logger
    
    
    #math
    def len_minus1(collection): return len(collection) - 1
    add = curry(lambda x,y:y+x)
    sub = curry(lambda x,y:y-x)
    mul = curry(lambda x,y:y*x)
    truediv = curry(lambda x,y:y/x)
    floordiv = curry(lambda x,y:y//x)
    pow = curry(lambda x,y:y**x)
    mod = curry(lambda x,y: y % x, arity=2))
    divisibleBy = lambda x: pipe(mod(x), eq(0))
    
    #function manipulation
    from functools import reduce
    pipe = lambda fn1,*fns: lambda arg,*args: reduce(lambda a,f: f(a), fns, fn1(arg,*args))
    # or, the verbose version
    def pipe(firstFn, *fns): 
        def pipeInner(lastArg,*args):
            lastArg = firstFn(lastArg,*args)
            for f in fns:
                lastArg = f(lastArg)
            return lastArg
        return pipeInner
    compose = lambda *fns :pipe(*reversed(fns))
    fmap = lambda fn: lambda data: (fn(d) for d in data)
    mapPipe = compose(fmap,pipe)
    spread = lambda fn : lambda iterableArg : fn(*iterableArg)
    forkjoin = lambda *fns,mergefn: lambda data:mergefn(*[fn(data) for fn in fns])
    nthArg = lambda argNum: lambda *args: args[argNum]
    negate = lambda fn: lambda *args,**kwargs:not fn(*args,**kwargs)
    over = lambda fns: lambda *args,**kwargs: [f(*args,**kwargs) for f in fns]
    def to_transformer(fn,acc):
      def inner(acc,v,k,c):
        fn(acc,v,k,c)
        return acc
      return inner
    transformTo = curry(lambda stubFn,fn,coll:reduce(to_transformer(fn),coll,stubFn()),arity=3)
    transToDict = transformTo(dict)
    listToArgs = lambda fn: lambda *lst,**kwargs: fn(*lst[0],**kwargs)
    argsToList = lambda fn: lambda *args,**kwargs: fn(args,**kwargs)
    
    from functools import partial
    def curry(fn,arity=2):
      if arity < 1: return fn
      def curryInner(*args,**kwargs):
        if len(args) >= arity : return fn(*args[:arity],**kwargs)
        return curry(partial(fn, *args[:arity],**kwargs), arity=arity-len(args))
      return curryInner
    
    # curry tests
    lt = curry(lambda x,y: x > y)
    assert lt(2,1) == True
    assert lt(2)(1) == True
    assert lt(2,1,100) == True
    assert lt(2)(1,100) == True
    assert lt()(2,1,100) == True
    
      
    # misc utils
    identity = lambda x: x
    noop = lambda *x: None
    constant = lambda x: lambda *ignored: x
    stub_0 = constant(0)
    stub_True = lambda *x: True
    stub_False = lambda *x: False
    stub_List = lambda *x: list()
    
    def assign_dicts(dest,*dicts):
      for d in dicts:
        for k in d.keys():
          dest[k]=d[k]
      return dest
    
    def assign_dicts(dest,*dicts):
      for d in dicts:
        for k in d.keys():
          dest[k]=d[k]
      return dest
    
    def analyze_graph(get_adjacent_vertices,collection}):
      graph = dict(
        vertices={id:dict(id=id,data=data) for v in get_adjacent_vertices('start',collection)},
        root_vertices={},
        in_edges={},
        in_paths={},
        out_edges={},
        in_cross={},
        out_cross={},
        in_back={},
        out_back={},
        in_forward={},
        out_forward={}
      )
    
      node = None
      queue=[v for v in graph['vertices']]
      while(len(queue)>0):
          node=queue.shift()
          for (id,data) in get_adjacent_vertices(node['id'],collection):
            if(id in graph['vertices']):
              pass # visited
              # tests for cross, back, forward edges
            else:
              graph['vertices'][id]=dict(id=id,data=data)
              queue.append()
    
      for (id,vertex) in graph['vertices'].items():
        if id not in graph['in_edges']:
          root_vertices[id]=vertex
              
      return graph

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
