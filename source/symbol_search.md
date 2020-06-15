---
title: symbol_search
date: 2020-05-07
---
Example Python program symbol_search.py

## Modules

* from atom.api import (Typed, ForwardTyped, Unicode, Bool, observe, set_default, ContainerList, Event)
* from enaml.core.declarative import d_
* from enaml.widgets.control import Control, ProxyControl
* from enaml.qt.qt_control import QtControl
* from qt_cw import QSymbolSearch

## Classes

* class ProxySymbolSearch(ProxyControl):
* class SymbolSearch(Control):
* class QtSymbolSearch(QtControl, ProxySymbolSearch):

## Methods

* def _update_proxy(self, change):
* def create_widget(self):
* def init_widget(self):
* def _enterPressed(self, code):
* def factory():

## Code

Python example

    
    from atom.api import (Typed, ForwardTyped, Unicode, Bool, observe, set_default, ContainerList, Event)
    from enaml.core.declarative import d_
    from enaml.widgets.control import Control, ProxyControl
    from enaml.qt.qt_control import QtControl
    from qt_cw import QSymbolSearch
    
    class ProxySymbolSearch(ProxyControl):
        declaration = ForwardTyped(lambda: SymbolSearch)
    
    class SymbolSearch(Control):
        proxy = Typed(ProxySymbolSearch)
        
        #enter pressed event
        enterPressed = d_(Event(str), writable=False)
    
        @observe()
        def _update_proxy(self, change):
            """ An observer which sends state change to the proxy.
            """
            # The superclass handler implementation is sufficient.
            super(SymbolSearch, self)._update_proxy(change)    
    
    class QtSymbolSearch(QtControl, ProxySymbolSearch):
        widget = Typed(QSymbolSearch)
        
        def create_widget(self):
            self.widget = QSymbolSearch(self.parent_widget())
    
        def init_widget(self):
            super(QtSymbolSearch, self).init_widget()
            self.widget.enterPressed.connect(self._enterPressed)
        
        def _enterPressed(self, code):
            self.declaration.enterPressed(code)
            
    
    def factory():
        return QtSymbolSearch 

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
