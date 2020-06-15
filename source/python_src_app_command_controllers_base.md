---
title: python_src_app_command_controllers_base
date: 2020-05-07
---
Example Python program python_src_app_command_controllers_base.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import os
* controller = __import__(path)

## Classes

* class BaseController:

## Methods

* def __init__ (self):
* def load (self, name):
* def home (self):
* def back (self, skip = 0):
* def exit (self):
* def input (

## Code

Python example

    import os
    
    class BaseController:
    
        _steps = []
    
    
        def __init__ (self):
            print 'BaseController.__init__()'
    
    
        def load (self, name):
            path = os.path.dirname(os.path.realpath(__file__)).replace(os.getcwd() + '/', '').replace('/', '.') + '.' + name
            controller = __import__(path)
            for p in path.split('.')[1:]:
                controller = getattr(controller, p)
    
            class_ = getattr(controller, name.capitalize() + 'Controller', None)
            if class_:
                class_()
            else:
                print 'Load Controller was failed ...'
                print('=' * 60)
                self.showOperations()
    
    
        def home (self):
            step = self._steps[0]
            self._steps = []
            self.input(**step)
    
    
        def back (self, skip = 0):
            # print '>> go back'
            self._steps.pop() # must be remove one
            if skip > 0 and skip < len(self._steps):
                for i in range(skip):
                    self._steps.pop()
            if len(self._steps) == 0:
                self.exit()
            self.input(**self._steps.pop())
    
    
        def exit (self):
            print 'Bye!'
            exit()
    
        def input (
            self,
            title = 'What you can do below:',
            operations = { '0': { 'do': 'exit' } },
            instance = None,
            *args,
            **whatever
        ):
            self._steps.append({ 'instance': instance or self, 'title': title, 'operations': operations  })
    
            theLast = self._steps[-1]
            instance = theLast['instance']
            operations = theLast['operations']
            title = theLast['title']
    
            while True:
                print ('-' * 60) + '\n' + title
    
                keys = operations.keys()
                keys.sort()
                for key in keys:
                    if ('name' in operations[key]):
                        name = operations[key]['name']
                    else:
                        name = operations[key]['do']
                    print('{0}. {1}'.format(key, name))
    
                do = raw_input('Please choose: ')
                print('>' * 60)
                if do in operations.keys() and 'do' in operations[do]:
                    # print(operations[do])
                    func = getattr(instance, operations[do]['do'], False)
                    if func:
                        if 'args' in operations[do]:
                            args = operations[do]['args']
                            argsType = type(args)
                            if argsType is tuple:
                                result = func(*args)
                            elif argsType is dict:
                                result = func(**args)
                            elif argsType is list:
                                result = func(*tuple(args))
                            else:
                                result = func(args)
                        else:
                            result = func()
                        print '<' * 60
                        if result == False:
                            break
                    else:
                        print 'Not Impletement!\n'
                else:
                    print 'Not support!\n'
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
