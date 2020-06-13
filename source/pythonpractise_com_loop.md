---
title: pythonpractise_com_loop
date: 2020-05-07
---
Example Python program pythonpractise_com_loop.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Code

Python example

    
    #while 循环
    
    
    n = 100
    
    sum = 0
    counter = 1
    while counter <= n:
        sum = sum + counter
        counter += 1
    
    print("1 到 %d 之和为: %d" % (n ,sum))
    
    
    languages = ["C", "C++", "Perl", "Python" , "java"]
    for x in languages:
        print(x)
    
    
    sites = ["Baidu", "Google","Runoob","Taobao"]
    for site in sites:
        if site == "Runoob":
            print("菜鸟教程!")
            break
        print("循环数据 " + site)
    else:
        print("没有循环数据!")
    print("完成循环!")
    
    
    print("=============================================")
    
    for i in range(10):
        print(i)
    
    print("=============================================")
    for i in range(5,9):
        print(i)
    
    #也可以使range以指定数字开始并指定不同的增量(甚至可以是负数，有时这也叫做'步长'):
    print("也可以使range以指定数字开始并指定不同的增量(甚至可以是负数，有时这也叫做'步长'):")
    
    for i in range(0, 10, 3) :
        print(i)
    
    print("===========================")
    
    for i in range(-20 , -100 , -10):
        print(i)
    
    
    #Python pass是空语句，是为了保持程序结构的完整性。
    #pass 不做任何事情，一般用做占位语句，如下实例
    
    for letter in "Runoob":
        if letter == 'o':
            pass
            print("执行pass")
        print("当前字母:" + letter)
    
    
    print("-------------------------------------------------")
    
    print("使用内置 enumerate 函数进行遍历:")
    sequence = [12, 34, 34, 23, 45, 76, 89]
    for i,j in enumerate(sequence):
        print(i,j)
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
