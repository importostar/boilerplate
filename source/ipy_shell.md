---
title: ipy_shell
date: 2020-05-07
---
Example Python program ipy_shell.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os
* import sys
* from PyQt5.QtCore import QUrl
* from PyQt5.QtGui import QPixmap, QPainter
* from PyQt5.QtQml import qmlRegisterType
* from PyQt5.QtQuick import QQuickView, QQuickPaintedItem
* from PyQt5.QtWidgets import QApplication
* from PyQt5 import QtWidgets
* from IPython.qt.console.rich_ipython_widget import RichIPythonWidget
* from IPython.qt.inprocess import QtInProcessKernelManager

## Classes

* class QIPythonWidget(RichIPythonWidget):
* class IPyShellQml(QQuickPaintedItem):

## Methods

* def get_app_qt5(*args, **kwargs):
* def __init__(self, customBanner=None, *args, **kwargs):
* def stop():
* def pushVariables(self, variableDict):
* def clearTerminal(self):
* def printText(self, text):
* def executeCommand(self, command):
* def __init__(self, parent=None):
* def keyPressEvent(self, event):
* def keyReleaseEvent(self, event):
* def paint(self, painter):
* def print_process_id():
* def main():

## Code

Example Python PyQt program :

    import os
    import sys
    
    from PyQt5.QtCore import QUrl
    from PyQt5.QtGui import QPixmap, QPainter
    from PyQt5.QtQml import qmlRegisterType
    from PyQt5.QtQuick import QQuickView, QQuickPaintedItem
    from PyQt5.QtWidgets import QApplication
    
    os.environ['QT_API'] = 'pyqt5'
    
    from PyQt5 import QtWidgets
    # ipython won't work if this is not correctly installed. And the error message will be misleading
    
    # Import the console machinery from ipython
    from IPython.qt.console.rich_ipython_widget import RichIPythonWidget
    from IPython.qt.inprocess import QtInProcessKernelManager
    
    
    def get_app_qt5(*args, **kwargs):
        """Create a new qt5 app or return an existing one."""
        app = QtWidgets.QApplication.instance()
        if app is None:
            if not args:
                args = ([''],)
            app = QtWidgets.QApplication(*args, **kwargs)
        return app
    
    
    class QIPythonWidget(RichIPythonWidget):
        """ Convenience class for a live IPython console widget. We can replace the standard banner using the customBanner argument"""
    
        def __init__(self, customBanner=None, *args, **kwargs):
            super(QIPythonWidget, self).__init__(*args, **kwargs)
            if customBanner != None: self.banner = customBanner
            self.kernel_manager = kernel_manager = QtInProcessKernelManager()
            kernel_manager.start_kernel()
            kernel_manager.kernel.gui = 'qt'
            self.kernel_client = kernel_client = self._kernel_manager.client()
            kernel_client.start_channels()
    
            def stop():
                kernel_client.stop_channels()
                kernel_manager.shutdown_kernel()
                get_app_qt5().exit()
    
            self.exit_requested.connect(stop)
    
        def pushVariables(self, variableDict):
            """ Given a dictionary containing name / value pairs, push those variables to the IPython console widget """
            self.kernel_manager.kernel.shell.push(variableDict)
    
        def clearTerminal(self):
            """ Clears the terminal """
            self._control.clear()
    
        def printText(self, text):
            """ Prints some plain text to the console """
            self._append_plain_text(text)
    
        def executeCommand(self, command):
            """ Execute a command in the frame of the console widget """
            self._execute(command, False)
    
    
    class IPyShellQml(QQuickPaintedItem):
        """ Main GUI Window including a button and IPython Console widget inside vertical layout """
    
        def __init__(self, parent=None):
            super(IPyShellQml, self).__init__(parent)
            self.setFlag(QQuickPaintedItem.ItemHasContents, True)
            self.ipyConsole = QIPythonWidget(customBanner="Welcome to the embedded ipython console\n")
            self.ipyConsole.pushVariables({"foo": 43, "print_process_id": print_process_id})
            self.ipyConsole.printText("The variable 'foo' and the method 'print_process_id()' are available."
                                      " Use the 'whos' command for information.\n\nTo push variables run this "
                                      "before starting the UI:"
                                      "\n ipyConsole.pushVariables({\"foo\":43,\"print_process_id\":print_process_id})")
    
        def keyPressEvent(self, event):
            self.ipyConsole.keyPressEvent(event)
    
        def keyReleaseEvent(self, event):
            self.ipyConsole.keyReleaseEvent(event)
    
        def paint(self, painter):
            painter.setRenderHints(QPainter.Antialiasing, True)
            rect = self.contentsBoundingRect()
            pix_map = QPixmap(rect.size().toSize())
            self.ipyConsole.render(pix_map)
            painter.drawPixmap(rect, pix_map, rect)
    
    
    def print_process_id():
        print('Process ID is:', os.getpid())
    
    
    def main():
        app = QApplication(sys.argv)
        qmlRegisterType(IPyShellQml, "IPython", 1, 0, "IPyShellQml")
        view = QQuickView(QUrl("ipy.qml"))
        view.setResizeMode(QQuickView.SizeRootObjectToView)
        view.resize(500, 500)
        view.show()
        app.exec_()
    
    
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
