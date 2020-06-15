---
title: pyqt_dbus
date: 2020-05-07
---
Example Python program pyqt_dbus.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from PyQt5.QtCore import QObject, pyqtSignal, QSharedMemory
* from PyQt5.QtWidgets import QApplication
* from PyQt5.QtWidgets import QMainWindow
* from PyQt5.QtWidgets import QPlainTextEdit
* from PyQt5.QtWidgets import QWidget
* from PyQt5.QtWidgets import QVBoxLayout
* from PyQt5.QtWidgets import QPushButton
* from PyQt5.QtCore import pyqtSlot, Q_CLASSINFO
* from PyQt5 import QtCore, QtDBus
* import simplejson as json
* import time
* import asyncio
* import multiprocessing as mp
* import concurrent.futures
* import functools
* from multiprocessing import Manager

## Classes

* class GatherDBusAdaptor(QtDBus.QDBusAbstractAdaptor):
* class GatherDBusInterface(QtDBus.QDBusAbstractInterface):
* class GatherSignal(QObject):
* class Gui(QMainWindow):
* class DataProcess():

## Methods

* 	def __init__(self, parent):
* 	def __init__(self, service, path, connection, parent=None):
* def __init__(self, parent=None, *args, **kwargs):
* def message(self, msg):
* def send(self, msg):
* def emit(self, data):
* def connect(self, method):
* def __init__(self, parent=None, *args, **kwargs):
* def setSignal(self, signal):
* def up_gui(self):
* def printhola(self):
* def print_log(self, msg):
* def update_data(self, msg):
* def run_gui(data):
* def __init__(self, *args, **kwargs):
* def run(self):

## Code

Example Python PyQt program :

    """
    Example with Signal-Slot system from QT
    When generate data, sends and load on the Gui's text widget
    
    """
    
    import sys
    from PyQt5.QtCore import QObject, pyqtSignal, QSharedMemory
    from PyQt5.QtWidgets import QApplication
    from PyQt5.QtWidgets import QMainWindow
    from PyQt5.QtWidgets import QPlainTextEdit
    from PyQt5.QtWidgets import QWidget
    from PyQt5.QtWidgets import QVBoxLayout
    from PyQt5.QtWidgets import QPushButton
    from PyQt5.QtCore import pyqtSlot, Q_CLASSINFO
    from PyQt5 import QtCore, QtDBus
    import simplejson as json
    #D-bus chapter
    
    class GatherDBusAdaptor(QtDBus.QDBusAbstractAdaptor):
    	Q_CLASSINFO("D-Bus Interface", "atlas.csn.gui")
    	Q_CLASSINFO("D-Bus Introspection", ''
    		'  <interface name="atlas.csn.gui">\n'
    		'	 <signal name="message">\n'
    		        '	   <arg direction="out" type="a{sv}" name="data"/>\n'
    		'	 </signal>\n'
    		'  </interface>\n'
    		'')	
    	message = pyqtSignal(dict)
    	def __init__(self, parent):
    		super().__init__(parent)
    		self.setAutoRelaySignals(True)
    
    class GatherDBusInterface(QtDBus.QDBusAbstractInterface):
    	message = pyqtSignal(dict)
    	def __init__(self, service, path, connection, parent=None):
    		super().__init__(service, path, 'atlas.csn.gui', connection, parent)
    
    class GatherSignal(QObject):
        signal=pyqtSignal(dict)
        def __init__(self, parent=None, *args, **kwargs):
            super().__init__(parent=parent)
            self.path="/"
            if 'path' in kwargs.keys():
                    self.path=kwargs['path']
            self.service = "atlas.csn.gui"
            if 'service' in kwargs.keys():
                    self.service=kwargs['service']
            self.variable = "message"
            if 'variable' in kwargs.keys():
                    self.variable=kwargs['variable']
            GatherDBusAdaptor(self)
            QtDBus.QDBusConnection.sessionBus().registerObject(self.path, self)
            self.connection=QtDBus.QDBusConnection.sessionBus()
            iface=GatherDBusInterface('', '', self.connection, self)
            self.connect(self.send)
        def message(self, msg):
            self.signal.emit(msg)
        @pyqtSlot(dict)
        def send(self, msg):
            assert type(msg)==dict, "Mensaje no es de tipo diccionario"
            data=msg#json.dumps(msg)
            print("send to dbus %s" %data)
            self.emit(data)
        def emit(self, data):
            msg = QtDBus.QDBusMessage.createSignal(self.path, self.service, self.variable)
            msg << data
            print(msg)
            self.connection.send(msg)
        def connect(self, method):
            self.signal.connect(method)
    
    class Gui(QMainWindow):
        message=pyqtSignal(dict)
        def __init__(self, parent=None, *args, **kwargs):
            super().__init__(parent)
            self.path="/"
            if 'path' in kwargs.keys():
                self.path=kwargs['path']
            self.service = "atlas.csn.gui"
            if 'service' in kwargs.keys():
                self.service=kwargs['service']
            self.variable = "message"
            if 'variable' in kwargs.keys():
                self.variable=kwargs['variable']
            #self.message.connect(self.update_data)
            #Connect to dbus
            GatherDBusAdaptor(self)
            #QtDBus.QDBusConnection.sessionBus().registerObject(self.path, self)
            self.connection=QtDBus.QDBusConnection.sessionBus()
            self.connection.registerObject(self.path, self)
            iface=GatherDBusInterface('', '', self.connection, self)
            print(iface)
            print(iface.message)
            #QtDBus.QDBusConnection.sessionBus().connect('', '',	self.service, self.variable, self.print_log)
            #self.connection.connect('', '',	self.service, self.variable, self.print_log)
            iface.message.connect(self.update_data)
            self.up_gui()
        def setSignal(self, signal):
            print("Signal %s" %signal)
            self.message=signal		
        def up_gui(self):
            main_widget=QWidget()
            layout=QVBoxLayout(main_widget)
            self.text=QPlainTextEdit()
            self.setCentralWidget(self.text)
            self.button=QPushButton('Print Hola')
            self.button.clicked.connect(self.printhola)
            layout.addWidget(self.button)
            layout.addWidget(self.text)
            self.setCentralWidget(main_widget)
            self.show()
        @pyqtSlot()
        def printhola(self):
            self.print_log("Hola\n")
        @pyqtSlot(dict)    
        def print_log(self, msg):
            print(msg)
            self.text.insertPlainText(json.dumps(msg))		
        @pyqtSlot(dict)
        def update_data(self, msg):
            data=msg
            print("Data received from dbus %s" %data)
            self.print_log(data)
     
    def run_gui(data):
    	app=QApplication(sys.argv)
    	gui=Gui(**data)
    	gui.showMaximized()
    	sys.exit(app.exec_())
    
    
    import time
    
    
    class DataProcess():
        def __init__(self, *args, **kwargs):
            super().__init__()
    
        def run(self):
            self.signal=GatherSignal()
            count=0
            while True:
                self.signal.message({'msg':"Hello %s" %count})
                time.sleep(2)
                count+=1
                if count>=100:
                    break
    
    
    import asyncio
    import multiprocessing as mp
    import concurrent.futures
    import functools
    
    from multiprocessing import Manager
    
    	
    if __name__ == "__main__":
        loop = asyncio.get_event_loop()
        workers = 2
        executor = concurrent.futures.ProcessPoolExecutor(workers)
        data = {"a":1}
        dp = DataProcess(**data)
        task_gui = loop.run_in_executor(executor,
                                        functools.partial(run_gui, data))
        task_dp = loop.run_in_executor(executor,
                                       dp.run)
        tasks=[task_gui, task_dp]
        loop.run_until_complete(asyncio.gather(**tasks))
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
