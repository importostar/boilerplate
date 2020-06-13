---
title: tk_wrapper
date: 2020-05-07
---
Example Python program tk_wrapper.py

## Modules

* >>> from tk_wrapper import interactive
* import Tkinter
* import inspect
* import sys
* import Tkinter

## Classes

* class interactive(object):

## Methods

* >>> def f(a,b=20):
* def __init__(self, func, title='title', **kwargs):
* def display(self):
* def status_change(self):
* def set_value(self, var, kw, new_value):
* def type_check(self, arg):
* def scale_bar(self, kw, arg, argtype):
* def scale_interact(new):
* def checkbutton(self, kw, arg):
* def check_interact():
* def radiobuttons_str(self, kw, arg):
* def select():
* def radiobuttons_dict(self, kw, arg):
* def select():
* def f(x, y, z, o=True, i=0):
* def b1():

## Code

Python tkinter example

    #! /usr/bin/env python
    # -*- coding:utf-8 -*-
    #
    # written by ssh0, October 2014.
    __doc__ = '''IPython-like Tkinter wrapper class.
    
    You can create Scalebar, Checkbutton, Radiobutton via simple interface.
    
    usage example:
    
    >>> from tk_wrapper import interactive
    >>> def f(a,b=20):
    ...     return a + b
    ...
    >>> w = interactive(f, a=(0, 20, 2), b=20)
    
    (in console, tk widget appear here)
    (you can add buttons and label here manually)
    
    (then, you should add the next line)
    >>> w.display()
    
    (and you can get the result for f(a,b) by)
    >>> w.result
    32
    
    (or get the arguments with a dictionary)
    >>> w.kwargs
    {'a':8, 'b':24}
    '''
    
    import Tkinter
    import inspect
    
    
    class interactive(object):
    
        def __init__(self, func, title='title', **kwargs):
            self.__doc__ = __doc__
            self.func = func
            self.kwargs = dict()
            args, varargs, keywords, defaults = inspect.getargspec(self.func)
            d = []
            for default in defaults:
                d.append(default)
            self.kwdefaults = dict(zip(args[len(args)-len(defaults):], d))
    
            self.root = Tkinter.Tk()
            self.root.title(title)
            self.f = Tkinter.Frame(self.root)
            for kw, arg in kwargs.items():
                kw = str(kw)
                arg_type = type(arg)
                if arg_type == tuple:
                    # type check for elements in tuple
                    argtype = self.type_check(arg)
                    if argtype == str:
                        self.radiobuttons_str(kw, arg)
                    else:
                        self.scale_bar(kw, arg, argtype)
                elif arg_type == int or arg_type == float:
                    self.scale_bar(kw, [arg], arg_type)
                elif arg_type == bool:
                    self.checkbutton(kw, arg)
                elif arg_type == str:
                    self.label(arg)
                    self.kwargs[kw] = arg
                elif arg_type == dict:
                    self.radiobuttons_dict(kw, arg)
                else:
                    raise TypeError
    
            self.f.pack()
            self.status = Tkinter.Label(self.root, text=str(self.kwargs))
            self.status.pack()
    
        def display(self):
            self.root.mainloop()
    
        def status_change(self):
            self.status.config(text=str(self.kwargs))
            self.kwargs_for_function = self.kwdefaults
            for k, v in self.kwargs.items():
                self.kwargs_for_function[k] = v
            self.result = self.func(**self.kwargs_for_function)
    
        def set_value(self, var, kw, new_value):
            # if argument is already given in func, use it for a default one
            if kw in self.kwdefaults:
                var.set(self.kwdefaults[kw])
                self.kwargs[kw] = self.kwdefaults[kw]
            else:
                var.set(new_value)
                self.kwargs[kw] = new_value
    
        def type_check(self, arg):
            argtype = type(arg[0])
            if not all([type(a) == argtype for a in arg]):
                raise TypeError("""types in a tuple must be the same.
                int or float: Scalebar
                str         : Radiobuttons""")
            return argtype
    
        def scale_bar(self, kw, arg, argtype):
    
            def scale_interact(new):
                self.kwargs[kw] = var.get()
                self.status_change()
    
            # length check for tuple
            len_arg = len(arg)
            if len_arg > 3 or len_arg == 0:
                raise IndexError("tuple must be 1 or 2 or 3 element(s)")
    
            if argtype == int:
                var = Tkinter.IntVar()
                scale_resolution = 1
            elif argtype == float:
                var = Tkinter.DoubleVar()
                scale_resolution = 0.1
            else:
                raise TypeError("arg must be int or float")
    
            # set the values
            if len_arg == 3:
                scale_from = arg[0]
                scale_to = arg[1]
                scale_resolution = arg[2]
            elif len_arg == 2:
                scale_from = arg[0]
                scale_to = arg[1]
            else:
                scale_from = arg[0]*(-1)
                scale_to = arg[0]*2
    
            self.set_value(var, kw, arg[0])
            # create scale widget in frame
            scale = Tkinter.Scale(self.f, label=kw, from_=scale_from, to=scale_to,
                                  resolution=scale_resolution, variable=var,
                                  orient='h', width=10, length=200,
                                  command=scale_interact)
            scale.pack()
    
        def checkbutton(self, kw, arg):
    
            def check_interact():
                self.kwargs[kw] = var.get()
                self.status_change()
    
            var = Tkinter.BooleanVar()
            self.set_value(var, kw, arg)
            checkbutton = Tkinter.Checkbutton(self.f, text=kw, variable=var,
                                              command=check_interact)
            checkbutton.pack()
    
        def radiobuttons_str(self, kw, arg):
    
            def select():
                self.kwargs[kw] = var.get()
                self.status_change()
    
            var = Tkinter.StringVar()
            label = Tkinter.Label(self.f, text='select one for '+kw)
            label.pack()
            self.set_value(var, kw, arg[0])
            for x in arg:
                R = Tkinter.Radiobutton(self.f, text=x, variable=var,
                                        value=x, command=select)
                R.pack()
    
        def radiobuttons_dict(self, kw, arg):
    
            def select():
                self.kwargs[kw] = var.get()
                self.status_change()
    
            vtype = self.type_check(arg.values())
            if vtype == str:
                var = Tkinter.StringVar()
            elif vtype == int:
                var = Tkinter.IntVar()
            elif vtype == float:
                var = Tkinter.DoubleVar()
            else:
                raise TypeError("arg must be int or float or str.")
            label = Tkinter.Label(self.f, text='select one for '+kw)
            label.pack()
            self.set_value(var, kw, arg.values()[0])
            for k, d in arg.items():
            
                R = Tkinter.Radiobutton(self.f, text=k, variable=var,
                                        value=d, command=select)
                R.pack()
    
    if __name__ == '__main__':
        import sys
        import Tkinter
    
        def f(x, y, z, o=True, i=0):
            print x, y, z, o, i
    
        def b1():
            print w.kwargs
    
        buttons = [('b1', b1), ('exit', sys.exit)]
        w = interactive(f, x=(0, 10), y=(1, 100, 10),
                        z=("ZZZ", "III", "foo", "bar"),
                        i={'0':0, '10':10, '20':20},
                        o=True
                        )
    
        for button in buttons:
            button = Tkinter.Button(w.root, text=button[0], command=button[1])
            button.pack()
    
        w.display()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
