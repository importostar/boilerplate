---
title: x
date: 2020-05-07
---
Example Python program x.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import attr

## Classes

* class Interface:
* class Left:
* class Right:

## Methods

* def create_interface(forward_connections, reverse_connections):
* def connect_forward(left, right):
* def connect_reverse(left, right):
* def connect(left, right):
* def reverse_slot_c(self):
* def do_something(self):
* def slot_a(self, text):
* def slot_b(self):

## Code

Example Python PyQt program :

    import attr
    
    
    @attr.s
    class Interface:
        left = attr.ib()
        right = attr.ib()
        connect_forward = attr.ib()
        connect_reverse = attr.ib()
        connect = attr.ib()
    
    
    def create_interface(forward_connections, reverse_connections):
        def connect_forward(left, right):
            for signal, slot in forward_connections.items():
                getattr(left, signal).connect(getattr(right, slot))
    
        def connect_reverse(left, right):
            for signal, slot in reverse_connections.items():
                getattr(right, signal).connect(getattr(left, slot))
        
        def connect(left, right):
            connect_forward(left, right)
            connect_reverse(left, right)
    
        Left = type(
            'Left',
            (PyQt5.QtCore.QObject,),
            {
                **{
                    name: PyQt5.QtCore.pyqtSignal('PyQt_PyObject')
                    for name in forward_connections.keys()
                },
            },
        )
    
        Right = type(
            'Right',
            (PyQt5.QtCore.QObject,),
            {
                **{
                    name: PyQt5.QtCore.pyqtSignal('PyQt_PyObject')
                    for name in reverse_connections.keys()
                },
            },
        )
        
        return Interface(
            left=Left,
            right=Right,
            connect_forward=connect_forward,
            connect_reverse=connect_reverse,
            connect=connect,
        )
    
    
    my_interface = create_interface(
        forward_connections={
            'signal_a': 'slot_a',
            'signal_b': 'slot_b',
        },
        reverse_connections={
            'reverse_signal_c': 'reverse_slot_c',
        },
    )
    
    @attr.s
    class Left:
        my_interface_signals = attr.ib(init=False, default=attr.Factory(my_interface.left))
    
        def reverse_slot_c(self):
            pass
        
        def do_something(self):
            self.my_interface_signals.signal_a.emit('hoo-ray')
    
    
    @attr.s
    class Right:
        my_interface_signals = attr.ib(init=False, default=attr.Factory(my_interface.right))
    
        def slot_a(self, text):
            print(text)
    
        def slot_b(self):
            pass
    
    left = Left()
    right = Right()
    
    my_interface.connect(left, right)
    left.do_something() # should print('hoo-ray')
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
