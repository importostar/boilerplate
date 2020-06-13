---
title: z
date: 2020-05-07
---
Example Python program z.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import attr
* import PyQt5.QtCore

## Classes

* class MissingSlotsError(Exception):
* class Connection:
* class Model:
* class View:
* class BadModel:

## Methods

* def create_interface(name, d):
* def apply(side_cls, cls):
* def __init__(self, *args, **kwargs):
* def connect(**kwargs):
* def disconnect(**kwargs):
* def reverse_slot_c(self):
* def do_something(self):
* def slot_a(self, text):
* def slot_b(self):

## Code

Example Python PyQt program :

    import attr
    import PyQt5.QtCore
    
    
    class MissingSlotsError(Exception):
        pass
    
    
    def create_interface(name, d):
        @classmethod
        def apply(side_cls, cls):
            other_side_name, = set(d) - {side_cls.__name__}
            missing_slots = [
                connection.slot
                for connection in d[other_side_name]
                if not hasattr(cls, connection.slot)
            ]
            
            if len(missing_slots) > 0:
                raise MissingSlotsError('{name} is missing slots: {slots}'.format(
                    name=cls.__name__,
                    slots=', '.join(missing_slots),
                ))
            
            old_init = cls.__init__
    
            def __init__(self, *args, **kwargs):
                setattr(self, name, side_cls())
                old_init(self, *args, **kwargs)
            
            cls.__init__ = __init__
            
            return cls
        
        sides = {
            name: type(
                name,
                (PyQt5.QtCore.QObject,),
                {
                    **{
                        connection.signal: PyQt5.QtCore.pyqtSignal(*connection.parameters)
                        for connection in connections
                    },
                    'apply': apply,
                },
            )
            for name, connections in d.items()
        }
    
        @staticmethod
        def connect(**kwargs):
            for side_name, connections in d.items():
                this = getattr(kwargs[side_name], name)
                that_name, = set(kwargs) - {side_name}
                that = kwargs[that_name]
                for connection in connections:
                    getattr(this, connection.signal).connect(getattr(that, connection.slot))
    
        @staticmethod
        def disconnect(**kwargs):
            for side_name, connections in d.items():
                this = getattr(kwargs[side_name], name)
                that_name, = set(kwargs) - {side_name}
                that = kwargs[that_name]
                for connection in connections:
                    getattr(this, connection.signal).disconnect(getattr(that, connection.slot))
    
        return type(
            name,
            (),
            {
                **sides,
                'connect': connect,
                'disconnect': disconnect,
            },
        )
    
    
    @attr.s
    class Connection:
        signal = attr.ib()
        slot = attr.ib()
        parameters = attr.ib()
    
    ModelViewInterface = create_interface(
        name='ModelViewInterface',
        d={
            'model': (
                Connection(signal='signal_a', slot='slot_a', parameters=(str,)),
                Connection(signal='signal_b', slot='slot_b', parameters=(str,)),
            ),
            'view': (
                Connection(signal='reverse_signal_c', slot='reverse_slot_c', parameters=(str,)),
            ),
        },
    )
    
    @ModelViewInterface.model.apply
    class Model:
        def reverse_slot_c(self):
            pass
        
        def do_something(self):
            self.ModelViewInterface.signal_a.emit('hoo-ray')
    
    
    @ModelViewInterface.view.apply
    class View:
        def slot_a(self, text):
            print(text)
    
        def slot_b(self):
            pass
    
    model = Model()
    view = View()
    
    ModelViewInterface.connect(model=model, view=view)
    print("should print 'hoo-ray'")
    model.do_something()
    ModelViewInterface.disconnect(model=model, view=view)
    print('should print nothing')
    model.do_something()
    
    
    @ModelViewInterface.model.apply
    class BadModel:
        pass
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
