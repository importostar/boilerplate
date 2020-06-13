---
title: testy (1)
date: 2020-05-07
---
Example Python program testy (1).py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import attr
* import PyQt5.QtCore
* import PyQt5.QtWidgets

## Classes

* class Container:
* class PyQtify:
* class SignalContainer(PyQt5.QtCore.QObject):
* class Class(cls):
* class P(PyQt5.QtCore.QObject):

## Methods

* def pyqtify(changed='changed'):
* def inner(cls):
* def _pyqtify_property(self, name=temp.name):
* def _pyqtify_property(
* def pyqtify_get(self, name):
* def pyqtify_set(self, name, value):
* def __attrs_post_init__(self):
* def pyqtify_c(self):
* def pyqtify_c(self, value):

## Code

Example Python PyQt program :

    import attr
    import PyQt5.QtCore
    import PyQt5.QtWidgets
    
    app = PyQt5.QtWidgets.QApplication([])
    
    
    class Container:
        pass
    
    
    @attr.s
    class PyQtify:
        fields = attr.ib(default=attr.Factory(Container))
    
    
    def pyqtify(changed='changed'):
        def inner(cls):
            class SignalContainer(PyQt5.QtCore.QObject):
                for field in attr.fields(cls):
                    locals()[field.name] = PyQt5.QtCore.pyqtSignal('PyQt_PyObject')
    
            temp = Container()
    
            class Class(cls):
                temp.before = set(locals())
                locals()[changed] = SignalContainer()
                __pyqtify__ = PyQtify()
    
                for _pyqtify_field in attr.fields(cls):
                    temp.name = _pyqtify_field.name
                    setattr(__pyqtify__.fields, temp.name, _pyqtify_field)
                    del _pyqtify_field
    
                    temp.signal = PyQt5.QtCore.pyqtSignal('PyQt_PyObject')
                    locals()[
                        '__pyqtify_signal_{}__'.format(temp.name)
                    ] = temp.signal
    
                    temp.override = getattr(
                        cls,
                        'pyqtify_{}'.format(temp.name),
                        None,
                    )
    
                    if temp.override is None:
                        @PyQt5.QtCore.pyqtProperty(
                            'PyQt_PyObject',
                            notify=temp.signal,
                        )
                        def _pyqtify_property(self, name=temp.name):
                            return self.pyqtify_get(name)
    
                        @_pyqtify_property.setter
                        def _pyqtify_property(
                                self,
                                value,
                                name=temp.name):
                            self.pyqtify_set(name, value)
    
                        locals()[temp.name] = _pyqtify_property
                        del _pyqtify_property
                    else:
                        locals()[temp.name] = temp.override
    
                def pyqtify_get(self, name):
                    return getattr(self.__pyqtify__.fields, name)
    
                def pyqtify_set(self, name, value):
                    if value != getattr(self.__pyqtify__.fields, name):
                        setattr(self.__pyqtify__.fields, name, value)
                        try:
                            getattr(self.changed, name).emit(value)
                        except RuntimeError:
                            pass
    
                temp.after = set(locals())
    
            # print(sorted(temp.after - temp.before))
    
            return Class
    
        return inner
    
    
    @pyqtify()
    @attr.s
    class P(PyQt5.QtCore.QObject):
        a = attr.ib()
        b = attr.ib()
        c = attr.ib()
    
        def __attrs_post_init__(self):
            super().__init__()
    
        @PyQt5.QtCore.pyqtProperty('PyQt_PyObject')
        def pyqtify_c(self):
            x = self.pyqtify_get('c')
            print('custom get c: {}'.format(x))
            return x
    
        @pyqtify_c.setter
        def pyqtify_c(self, value):
            print('custom set c: {}'.format(value))
            return self.pyqtify_set('c', value)
    
    
    p = P(a=1, b=2, c=3)
    p.changed.a.connect(lambda x: print('a changed to {}'.format(x)))
    p.changed.b.connect(lambda x: print('b changed to {}'.format(x)))
    p.changed.c.connect(lambda x: print('c changed to {}'.format(x)))
    p.b = 42
    p.b = 42
    p.b = 37
    p.a = 12
    p.a = 12
    p.a = 13
    # print(p.pyqtify_c)
    print(p.c)
    p.c = 4
    print(attr.asdict(p))
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
