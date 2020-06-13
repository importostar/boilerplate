---
title: python_src_models_user
date: 2020-05-07
---
Example Python program python_src_models_user.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* # dbs = __import__('db', fromlist=['pickle', 'file'])
* # import uuid

## Classes

* class User:

## Methods

* def __init__ (self, **values):
* # def add():
* # def list():

## Code

Python example

    # dbs = __import__('db', fromlist=['pickle', 'file'])
    # db = getattr(dbs, 'pickle')
    
    
    class User:
    
        __slots__ = ['name', 'age']
    
        def __init__ (self, **values):
            print 'User.__init__()'
            print __class__
    
        # def add():
        #     user = {};
        #     user['name'] = raw_input('name?\n')
        #     user['age'] = input('age?\n')
        #
        #     import uuid
        #     id = uuid.uuid1()
        #     data = db.load('./data/user')
        #     data[id] = user
        #     if db.save('./data/user', data):
        #         print 'data is saved.'
        #     else:
        #         print 'data save failed'
        #
        #
        # def list():
        #     data = db.load('./data/user')
        #     if len(data) == 0:
        #         print None
        #     else:
        #         for id in data:
        #             print id
        #             print data[id]
        #             print '------------------------------'
        #     print '\r'
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
