---
title: pythonize
date: 2020-05-07
---
Example Python program pythonize.py

## Modules

* import importlib
* import pkgutil
* module = importlib.import_module(full_name)
* import sys
* import PyQt5

## Classes

* class ClassProxy(object):
* class _ModuleProxy(object):
* class _PackageProxy(object):

## Methods

* def pythonize(qt_package):
* def _make_class_proxy(qt_klass):
* def __init__(self, *args, **kwargs):
* def __getattr__(self, name):
* def __init__(self, module):
* def __getattr__(self, name):
* def __init__(self, package):

## Code

Example Python PyQt program :

    # ↓↓↓ Scroll to bottom for an example. ↓↓↓
    
    import importlib
    import pkgutil
    
    
    def pythonize(qt_package):
        proxy = _PackageProxy(qt_package)
        return proxy
    
    
    def _make_class_proxy(qt_klass):
    
        class ClassProxy(object):
    
            def __init__(self, *args, **kwargs):
                super(ClassProxy, self).__init__()
                self.__backend = qt_klass(*args, **kwargs)
    
            def __getattr__(self, name):
                # Convert Pythonic attribute names to camel case names.
                if name[0].islower():
                    # this_is_an_attribute => thisIsAnAttribute
                    comps = name.split('_')
                    comps = comps[:1] + [c.title() for c in comps[1:]]
                else:
                    # THIS_IS_A_CONSTANT => ThisIsAConstant
                    comps = [c.title() for c in name.split('_')]
                name = ''.join(comps)
                return getattr(self.__backend, name)
    
        return ClassProxy
    
    
    class _ModuleProxy(object):
    
        def __init__(self, module):
            super(_ModuleProxy, self).__init__()
            self.module = module
    
        def __getattr__(self, name):
            try:
                qt_klass = getattr(self.module, name)
            except AttributeError:
                qt_klass = getattr(self.module, 'Q' + name)
            proxy = _make_class_proxy(qt_klass)
            return proxy
    
    
    class _PackageProxy(object):
    
        def __init__(self, package):
            prefix = package.__name__ + '.'
            path = package.__path__
            for _, full_name, _ in pkgutil.iter_modules(path, prefix):
                name = full_name.split('.')[-1]
                if name.startswith('Qt'):
                    # Modules like QtCore, QtGui, QtWidgets, etc.
                    # Strip "Qt" prefix, convert to lower (i.e. core, gui, widgets)
                    # Note that multiword modules won't contain underscores. For
                    # example "QtPrintSupport" will become "printsupport".
                    local_name = name[2:].lower()
                elif name[0].isupper():
                    # Modules without the "Qt" prefix (e.g. Enginio)
                    local_name = name.lower()
                elif name[0] == '_':
                    # Private module. Skip.
                    continue
                else:
                    # Normal packages. Use as-is.
                    local_name = name
                module = importlib.import_module(full_name)
                proxy = _ModuleProxy(module)
                # Inject this into the local scope.
                setattr(self, local_name, proxy)
    
    
    # I'm testing with PyQt5. Rewrite where appropriate.
    import sys
    import PyQt5
    qt = pythonize(PyQt5)
    app = qt.widgets.Application(sys.argv)
    w = qt.widgets.MainWindow()
    w.show()
    app.exec_()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
