---
title: dict2obj
date: 2020-05-07
---
Example Python program dict2obj.py


## Classes

* class dict_to_obj(dict):

## Methods

* def __getattr__(self, name):
* def __setattr__(self, name, value):
* def __delattr__(self, name):

## Code

Python example

    class dict_to_obj(dict):
        def __getattr__(self, name):
            if name in self:
                return self[name]
            else:
                raise AttributeError("No such attribute: " + name)
    
        def __setattr__(self, name, value):
            self[name] = value
    
        def __delattr__(self, name):
            if name in self:
                del self[name]
            else:
                raise AttributeError("No such attribute: " + name)
    
    _quote = {
            "data": [
                    {"date": 1428289200000, "price": 5.05, "low": 5.01, "high": 5.11, "open": 5.05},
                    {"date": 1427943600000, "price": 5, "low": 4.88, "high": 5.05, "open": 4.93},
                    {"date": 1427857200000, "price": 4.91, "low": 4.91, "high": 5.07, "open": 5.01},
                    {"date": 1427770800000, "price": 4.97, "low": 4.97, "high": 5.14, "open": 5.1},
                    {"date": 1427684400000, "price": 5.12, "low": 5.12, "high": 5.24, "open": 5.18}
            ],
            "total": 5,
            "lastUpdate": 1435608300000,
            "type": "stock",
            "timeOffSet": -10800000,
            "today": 1435697531409
    }
    
    >>> quotes = dict_to_obj(_quote)
    >>> quotes.today
    1435697531409L
    >>> quotes.total
    5
    >>> quotes.data[0].date
    1428289200000L
    >>> quotes.data[0].price
    5.05
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
