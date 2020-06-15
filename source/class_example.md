---
title: class_example
date: 2020-05-07
---
Example Python program class_example.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from abc import ABC, abstractmethod
* import numpy as np

## Classes

* class Line:
* class Prampara(ABC):
* if child_class is Prampara:
* class Parent(Prampara):

## Methods

* def __set__(self, instance, value):
* def __get__(self, instance, owner):
* def __set_name__(self, owner, name):
* def function_one(cls):
* def function_two(cls):
* def function_three():
* def function_four():
* def descriptor(self):
* def __subclasshook__(cls, child_class):
* def __new__(cls, *args, **kwargs):
* def __init__(self, *args, **kwargs):
* def __del__(self):
* def __repr__(self) -> str:
* def __str__(self) -> str:
* def __bytes__(self) -> bytes:
* def __lt__(self, other) -> bool:
* def __le__(self, other) -> bool:
* def __gt__(self, other) -> bool:
* def __ge__(self, other) -> bool:
* def __eq__(self, other) -> bool:
* def __ne__(self, other) -> bool:
* def __hash__(self) -> int:
* def __bool__(self) -> bool:
* def __getattribute__(self, attribute):
* def __getattr__(self, attribute):
* def __setattr__(self, name, value):
* def __delattr__(self, name):
* def __dir__(self):
* # def __add__(self, other):
* def descriptor(self):
* def main():

## Code

Python example

    #!/usr/bin/python3
    
    """
        Python Data Model
    """
    
    from abc import ABC, abstractmethod
    import numpy as np
    
    
    class Line:
        """
            Descriptor class
        """
        points = []
    
        def __set__(self, instance, value):
            print("__set__")
            Line.points = value
    
        def __get__(self, instance, owner):
            print("__get__")
            return np.sqrt((Line.points[0][0] - Line.points[1][0]) ** 2 - (Line.points[0][1] - Line.points[1][1]) ** 2)
    
        def __set_name__(self, owner, name):
            print(f"Owner: {owner} -> Name: {name}")
    
    
    class Prampara(ABC):
        """
            Abstract Base class
        """
    
        @classmethod
        def function_one(cls):
            """
            Class Function One
            """
            print("Prampara -> function_one (classmethod)")
    
        @classmethod
        def function_two(cls):
            """
            Class Function Two
            """
            print("Prampara -> function_two (classmethod)")
    
        @staticmethod
        def function_three():
            """
            Static Function One
            """
            print("Prampara -> function_three (staticmethod)")
    
        @staticmethod
        def function_four():
            """
            Static Function Two
            """
            print("Prampara -> function_four (staticmethod)")
    
        @abstractmethod
        def descriptor(self):
            """
            Abstract Function
            """
    
        @classmethod
        def __subclasshook__(cls, child_class):
            if child_class is Prampara:
                if any("abstract_function" in base.__dict__ for base in child_class.__mro__):
                    pass
    
    
    class Parent(Prampara):
        """
        Parent Class
        """
    
        __slots__ = ['args']
    
        def __new__(cls, *args, **kwargs):
            """
                Creates new instance of the class
            """
            print(f"{kwargs['name']}: __new__")
    
            obj = super(Parent, cls).__new__(cls)
    
            if kwargs['invert_neg']:
                args = list(map(abs, args))
    
            obj.args = args
    
            return obj
    
        def __init__(self, *args, **kwargs):
            """
                Intialize array using random data from -100 to 100
            """
            super(Parent, self).__init__()
    
            _ = args
            self.later = None 
            self.name = kwargs['name']
    
            print(f"{self.name}: __init__({self.args})")
    
        def __del__(self):
            """
                Called when instance is about to be destroyed
            """
            print(f"{self.__class__.__name__}'s {self.name}: __del__")
    
        def __repr__(self) -> str:
            """
                Object's official string representation
            """
            return f"Parent's {self.name}"
    
        def __str__(self) -> str:
            """
                User readable string Repesentation
            """
            return f"Class: Parent; Object: {self.name}; Argument: {self.args}"
    
        def __bytes__(self) -> bytes:
            """
                Called by bytes to compute a byte-string representation of an object
            """
            return bytes(self.args)
    
        def __lt__(self, other) -> bool:
            """
                for self < other
            """
            return self.args < other.args
    
        def __le__(self, other) -> bool:
            """
                for self <= other
            """
            return self.args <= other.args
    
        def __gt__(self, other) -> bool:
            """
                for self > other
            """
            return self.args > other.args
    
        def __ge__(self, other) -> bool:
            """
                for self >= other
            """
            return self.args >= other.args
    
        def __eq__(self, other) -> bool:
            """
                for self == other
            """
            return self.args == other.args
    
        def __ne__(self, other) -> bool:
            """
                for self != other
            """
            return self.args != other.args
    
        def __hash__(self) -> int:
            """
                returns hash value
            """
            return hash(f"{self.name}: {self.args}")
    
        def __bool__(self) -> bool:
            """
                returns boolean value
            """
            return self.args > 100
    
        def __getattribute__(self, attribute):
            """
                called for every attribute regardless whether it exists or not
            """
            print(f"__getattribute__: ", end='')
    
            return super().__getattribute__(attribute)
    
        def __getattr__(self, attribute):
            """
                handles attribute error
    
            Parameters
            ----------
            attribute : object
                missing attribute
            
            Returns
            -------
            number
                return value
            """
            print("__getattr__: ", end='')
    
            self.__dict__[attribute] = 0
    
            return 0
    
        def __setattr__(self, name, value):
            """
                Called when an attribute assignment is attempted
    
            Parameters
            ----------
            name : {str}
                attribute name
            value : {object}
                attribute value
            """
            print("__setattr__: ")
    
            self.__dict__[name] = abs(value) if isinstance(value, (int, float)) else value
    
        def __delattr__(self, name):
            """
                Called for attribute deletion
    
            Parameters
            ----------
            name : {[type]}
                [description]
            """
            print(f"__delattr__({name}) : ")
            del self.__dict__[name]
    
        def __dir__(self):
            """
                returns attribute list
            """
            return [1, 2, 3]
    
        # def __add__(self, other):
        #     """
        #         for self + other
    
        #     Parameters
        #     ----------
        #     other : {[type]}
        #         [description]
        #     """
        #     return 
    
        # Calling Descriptor class
        line = Line()
    
        def descriptor(self):
            """
            Overridden function
            """
            Parent.line = ((0, 0), (2, 2))
    
            return Parent.line
    
    
    def main():
        """
        Main Function
        """
        parent_one = Parent(5, -20, invert_neg=True, name='parent_one')
        parent_two = Parent(-50, 100, invert_neg=True, name='parent_two')
    
        print(f"__repr__: {repr(parent_one)}")
        print(f"__repr__: {repr(parent_two)}")
    
        print(f"__str__: {parent_one}")
        print(f"__str__: {parent_two}")
    
        print(f"__bytes__: {bytes(parent_one)}")
        print(f"__bytes__: {bytes(parent_two)}")
    
        print(f"__lt__: {parent_one < parent_two}")
        print(f"__le__: {parent_one <= parent_two}")
        print(f"__gt__: {parent_one > parent_two}")
        print(f"__ge__: {parent_one >= parent_two}")
        print(f"__eq__: {parent_one == parent_two}")
        print(f"__ne__: {parent_one != parent_two}")
    
        print(f"__hash__: {hash(parent_one)}")
        print(f"__hash__: {hash(parent_two)}")
    
        print(f"__bool__: {bool(parent_one)}")
        print(f"__bool__: {bool(parent_two)}")
    
        # __getattribute__
        print(parent_one.args)
        print(parent_two.args)
    
        # __getattr__
        print(parent_one.argument)
        print(parent_two.argument)
    
        # __setattr__
        parent_one.later = [1, 'A']
        parent_one.later = [2, 'B']
    
        # __delattr__
        del parent_one.later
        del parent_two.later
    
        print(f"dir(parent_one): {dir(parent_one)}")
        print(f"dir(parent_two): {dir(parent_two)}")
    
        print(f"Descriptor: {parent_one.descriptor()}")
    
    
    if __name__ == "__main__":
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
