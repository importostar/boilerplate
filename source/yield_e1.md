---
title: yield_e1
date: 2020-05-07
---
Example Python program yield_e1.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Methods

* def yield_kim(n): # 0 1
* def yield_kim2(n):
* def yield_t1():

## Code

Python example

    # -*- coding: utf-8 -*-
    
    ## for 循环调用
    ## 第一次循环 n = 2, i = 0; yield i*2 = 0 打印 for i = 0 ,停在这个位置
    ## 第二次循环 执行下一个语句执行，打印 after i = 0 ； i= 1 满足循环条件 yield i*=2 ,打印 for i = 2
    ## 第三次循环 执行下一个语句执行，打印 after i = 1； i= 2 不满足循环条件 退出 。打印 others
    def yield_kim(n): # 0 1
        for i in range(n):
            yield i*2  # yield就类似 return 返回一个值，并且记住这个返回的位置，下次迭代就从这个位置后开始
            print("after i=",i)
        print("<--------------Others-------------->")
    
    ## for cycle
    for i in yield_kim(2): 
        print("for i=",i)
        
    #第一次输出  for i = 0
    #第二次输出  after i= 0
    #第二次输出  for i= 2
    #第三次输出  after i= 1
    #第三次输出  <--------------Others-------------->
    
        
    ## 普通调用----------------------
    def yield_kim2(n):
        print("n =",n) 
        a = yield n*2
        print("a = ",a)
        
    k = yield_kim2(2)
    k2 = next(k)   # 执行后 yield n*2 表达式的值为 4 ，a 还未赋值
    
    # 输出: n = 2
    
    
    ## yield 实战1, send(msg),next()
    def yield_t1():
        print("study yield")
        m = yield 5  # 常量 5
        print(m)
        d = yield 10
        print(d)
        f = yield 15
        print("last")
    
    c_val = yield_t1()              # 函数赋值
    s_d1 = next(c_val)              # 相当于send(None) ,m = yield 5; m = 5; s_d1 = 5
    s_d2 = c_val.send("Fighting!")  # (yield 5)表达式被赋予了'Fighting!' ，打印 m 值，运行到下一个 yield，并赋值 s_d2 = 10
    s_d3 = c_val.send("try Fight")  # (yield 10)表达式被赋予了'try Fight!'，打印 d 值， 运行到下一个 yield，并赋值 s_d3 = 15； 退出
    print("My DAY:",s_d1,"-",s_d2,"-",s_d3)
    
    #输出: study yield
    #输出: Fighting!
    #输出: try Fight
    #输出: My DAY: 5 - 10 - 15

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
