---
title: formloader
date: 2020-05-07
---
Example Python program formloader.py

## Modules

* Installs a python importlib PathFinder that assists with compiling and loading
* import importlib
* import io
* import logging
* import sys
* from PyQt5 import QtCore, uic
* class FormLoader(importlib.machinery.SourceFileLoader):
* class FormFileFinder(importlib.machinery.FileFinder):
* class FormFinder(importlib.machinery.PathFinder):

## Classes

* class FormLoader(importlib.machinery.SourceFileLoader):
* class FormFileFinder(importlib.machinery.FileFinder):
* class FormFinder(importlib.machinery.PathFinder):

## Methods

* def get_data(self, path):
* def __init__(self, path):
* def find_spec(cls, fullname, path=None, target=None):
* def install():

## Code

Example Python PyQt program :

    """
    Installs a python importlib PathFinder that assists with compiling and loading
    PyQt5 .ui files as python modules.
    """
    import importlib
    import io
    import logging
    import sys
    
    from PyQt5 import QtCore, uic
    
    
    logger = logging.getLogger(__name__)
    
    
    class FormLoader(importlib.machinery.SourceFileLoader):
    
        def get_data(self, path):
            """Return the data from path as raw bytes."""
            if path.endswith('.ui'):
                buf = io.StringIO()
                with buf, open(path, 'rb') as uifile:
                    uic.compileUi(uifile, buf)
                    return buf.getvalue().encode('utf-8')
            else:
                return super().get_data(path)
    
    
    class FormFileFinder(importlib.machinery.FileFinder):
    
        def __init__(self, path):
            super().__init__(path, (FormLoader, ('.ui',)))
    
    
    class FormFinder(importlib.machinery.PathFinder):
    
        @classmethod
        def find_spec(cls, fullname, path=None, target=None):
            if path:
                finder = FormFileFinder(path[0])
                spec = finder.find_spec(fullname, target=target)
                if spec is not None:
                    return spec
    
    
    def install():
        sys.meta_path.insert(0, FormFinder)
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
