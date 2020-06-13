---
title: reloadall
date: 2020-05-07
---
Example Python program reloadall.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import types
* from imp import reload
* import reloadall
* >>> from reloadall import reload_all
* >>> import os, tkinter

## Methods

* def status(module):
* def transitive_reload(module, visited):
* def reload_all(*args):

## Code

Python tkinter example

    """
    reloadall.py: транзитивная перезагрузка вложенных модулей
    """
    import types
    from imp import reload
    
    # требуется в версии 3.0
    def status(module):
        print('reloading' + module.__name__)
    
    def transitive_reload(module, visited):
        if not module in visited:
            # Пропустить повторные посещения
            status(module)
            # Перезагрузить модуль
            reload(module)
            # И посетить дочерние модули
            visited[module] = None
                for attrobj in module.__dict__.values(): # Для всех атрибутов
                    if type(attrobj) == types.ModuleType: # Рекурсия, если модуль
                        transitive_reload(attrobj, visited)
    
    def reload_all(*args):
        visited = {}
        for arg in args:
            if type(arg) == types.ModuleType:
                transitive_reload(arg, visited)
    
    if __name__ == '__main__':
        import reloadall
        reload_all(reloadall)
    # Тест: перезагрузить самого себя
    # Должна перезагрузить э
    
    """ 
    Вывод
    >>> from reloadall import reload_all
    >>> import os, tkinter
    >>> reload_all(os)
    reloading os
    reloading copyreg
    reloading ntpath
    reloading genericpath
    reloading stat
    reloading sys
    reloading errno
    >>> reload_all(tkinter)
    reloading tkinter
    reloading _tkinter
    reloading tkinter._fix
    reloading sys
    reloading ctypes
    reloading os
    reloading copyreg
    reloading ntpath
    reloading genericpath
    reloading stat
    reloading errno
    reloading ctypes._endian
    reloading tkinter.constants
    
    """
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
