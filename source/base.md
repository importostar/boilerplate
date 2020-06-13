---
title: base
date: 2020-05-07
---
Example Python program base.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import pickle
* import itertools
* from datetime import date, timedelta, datetime

## Code

Python example

    ##### lambda in list comprehension
    [(lambda x: x*x)(x) for x in range(10)]
    
    ##### remove an item from a list in python (clear, pop, remove, del)
    
    ## clear
    l = list(range(10))
    print(l)
    # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    
    l.clear()
    print(l)
    # []
    
    ## pop
    l = list(range(10))
    print(l)
    # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    
    print(l.pop(0))
    # 0
    
    print(l)
    # [1, 2, 3, 4, 5, 6, 7, 8, 9]
    
    print(l.pop(3))
    # 4
    
    print(l)
    # [1, 2, 3, 5, 6, 7, 8, 9]
    
    ## del
    l = list(range(10))
    print(l)
    # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    
    del l[0]
    print(l)
    # [1, 2, 3, 4, 5, 6, 7, 8, 9]
    
    
    
    ##### create dict from list of keys and values
    
    L1 = ['a','b','c','d']
    L2 = [1,2,3,4]
    d = dict(zip(L1,L2))
    ## or
    d = {k:v for k,v in zip(L1,L2)}
    
    ## {'a': 1, 'b': 2, 'c': 3, 'd': 4}
    
    ##### path string on windows
    
    ## 'C:/mydir'
    ## 'C:\\mydir'
    ## r'C:\mydir'
    os.path.join(mydir, myfile)
    
    ##### extract number from str list
    mystr = ['F11', 'F22']
    [int(re.findall('\d+', x)[0]) for x in mystr]
    
    ##### string format method
    
    ### older
    
    print('%d %.2f %s' % (1, 99.3, 'Justin'))
    1 99.30 Justin
    
    ## %%  to display '%'
    ## %d  to display int (decimal)
    ## %e  to display float (decimal, scientific notation)
    ## %f  to display float 
    ## %s  to display str
    ## #r  to display str(repr)
    
    ### new
    name = 'Jack'
    text = 'world'
    
    print('hello {name}, hello {text}'.format(name=name, text=text))
    
    
    ##### pickle operation
    
    import pickle
    a_dict = {'da': 111, 2: [23,1,4], '23': {1:2,'d':'sad'}}
    
    ## save pickle
    
    file = open('pickle_example.pickle', 'wb')
    pickle.dump(a_dict, file)
    file.close()
    
    ## load pickle
    # reload a file to a variable
    with open('pickle_example.pickle', 'rb') as file:
        a_dict1 =pickle.load(file)
    print(a_dict1)
    
    
    ##### repeat elements of a list for n times
    
    ## in base
    import itertools
    lst = range(1,5)
    list(itertools.chain.from_iterable(itertools.repeat(x, 3) for x in lst))
    
    [1, 1, 1, 2, 2, 2, 3, 3, 3, 4, 4, 4]
    
    ## numpy way
    x = [1, 2, 3, 4]
    np.repeat(x, 3)
    
    [1, 1, 1, 2, 2, 2, 3, 3, 3, 4, 4, 4]
    
    ##### datetime type time delta (minus or plus)
    from datetime import date, timedelta, datetime
    dt = datetime.strptime('20200501', "%Y%m%d")
    (dt - timedelta(days=1)).strftime("%Y%m%d"")
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
