---
title: python_src_utils_storage_file (1)
date: 2020-05-07
---
Example Python program python_src_utils_storage_file (1).py


## Methods

* def load (name, ext='.txt'):
* def save (name, data=[], ext='.txt'):

## Code

Python example

    ENDDB = 'enddb.'
    ENDREC = 'endrec.'
    RECSEP = '=>'
    
    
    def load (name, ext='.txt'):
        data = {}
        try:
            with open(name + ext, 'r') as file:
                key = file.readline().rstrip()
                while key != ENDDB and len(key) > 0:
                    rec = {}
                    field = file.readline().rstrip()
                    while field != ENDREC:
                        name, value = field.split(RECSEP)
                        rec[name] = eval(value)
                        field = file.readline().rstrip()
                    data[key] = rec
                    key = file.readline().rstrip()
        except IOError:
            pass
        return data
    
    
    def save (name, data=[], ext='.txt'):
        try:
            with open(name + ext, 'w') as file:
                for id in data:
                    print >> file, id
                    for (key, value) in data[id].items():
                        print >> file, key + RECSEP + repr(value)
                    print >> file, ENDREC
                print >> file, ENDDB
        except IOError:
            return False
        return True
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
