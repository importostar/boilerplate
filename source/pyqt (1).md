---
title: pyqt (1)
date: 2020-05-07
---
Example Python program pyqt (1).py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5 import QtCore, QtWidgets, QtGui
* from PyQt5.uic import compileUi

## Classes

* class XStream(QtCore.QObject):
* class QtHandler(logging.Handler):
* class ApplicationWindow(Ui_CalibWindow, QtWidgets.QMainWindow):

## Methods

* def flush( self ) : pass
* def fileno( self ): return -1
* def write( self, msg ):
* def stdout():
* def stderr():
* def __init__(self):
* def emit(self, record):
* def __init__(self):

## Code

Example Python PyQt program :

    import sys
    # Make sure that we are using QT5
    matplotlib.use('Qt5Agg')
    from PyQt5 import QtCore, QtWidgets, QtGui
    
    class XStream(QtCore.QObject):
        """ used to redirect iostream sys.stdout to qt signal 
        Example:
            XStream.stdout().messageWritten.connect( self.logTxt.insertPlainText )
            XStream.stderr().messageWritten.connect( self.logTxt.insertPlainText )
        """
        _stdout = None
        _stderr = None
        messageWritten = QtCore.pyqtSignal(str)
        def flush( self ) : pass
        def fileno( self ): return -1
        def write( self, msg ):
            if not self.signalsBlocked() :
                self.messageWritten.emit(msg)
        @staticmethod
        def stdout():
            if not XStream._stdout :
                XStream._stdout = XStream()
                sys.stdout = XStream._stdout
            return XStream._stdout
        @staticmethod
        def stderr():
            if not XStream._stderr :
                XStream._stderr = XStream()
                sys.stderr = XStream._stderr
            return XStream._stderr
        
    class QtHandler(logging.Handler):
        """ used to redirect logging output  
        """
        def __init__(self):
            logging.Handler.__init__(self)
        def emit(self, record):
            record = self.format(record)
            if record: XStream.stdout().write('%s\n'%record)
        
    logger = logging.getLogger()
    handler = QtHandler()
    handler.setFormatter(logging.Formatter("%(levelname)s: %(message)s"))
    logger.addHandler(handler)
    logger.setLevel(logging.INFO) # DEBUG
    
    
    
    #%%%  how to use ui file from qtcreator in PyQt5
    from PyQt5.uic import compileUi
    class ApplicationWindow(Ui_CalibWindow, QtWidgets.QMainWindow):
        def __init__(self):
            super(ApplicationWindow, self).__init__()
            self.setupUi(self)
            ....
            
    app_created = False
    app = QtCore.QCoreApplication.instance()
    if app is None:
        app = QtWidgets.QApplication(sys.argv)
        app_created = True
    app.references = set()
    window = ApplicationWindow()
    app.references.add(window)
    window.show()
    if app_created:
        app.exec_()        

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
