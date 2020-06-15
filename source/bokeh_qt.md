---
title: bokeh_qt
date: 2020-05-07
---
Example Python program bokeh_qt.py
This program creates a PyQt GUI

## Modules

* There are 2 lines of code and 1 import that are not part of the standard boilerplate.
* from PyQt5 import QtWebEngineWidgets
* import sys
* from PyQt5 import QtCore, QtGui, QtWidgets
* from PyQt5.QtWidgets import QMainWindow
* from PyQt5 import QtWebEngineWidgets

## Classes

* class WebViewWindow(QMainWindow):

## Methods

* def __init__(self, url):

## Code

Example Python PyQt program :

    """
    The follow short app is a minimal example of rendering web-content in PyQt.  This code is not
    Bokeh-specific, but is a working example capable of rendering a Bokeh application.
    
    It uses the newer QtWebEngine rather than the now deprecated QtWebKit.  This has the side-effect
    of not working  out of the gate with PyQt4.  However PyQt4 / QtWebEngine should be sufficient to
    render a Bokeh application.
    
    There are 2 lines of code and 1 import that are not part of the standard boilerplate.
            from PyQt5 import QtWebEngineWidgets
            self.web_view = QtWebEngineWidgets.QWebEngineView()
            self.web_view.setUrl(QtCore.QUrl(url))
    
    Everything else is more or less identical to any basic PyQt example.
    """
    
    import sys
    from PyQt5 import QtCore, QtGui, QtWidgets
    from PyQt5.QtWidgets import QMainWindow
    from PyQt5 import QtWebEngineWidgets
    
    
    class WebViewWindow(QMainWindow):
    
        def __init__(self, url):
            QMainWindow.__init__(self)
            self.web_view = QtWebEngineWidgets.QWebEngineView()
            self.web_view.setUrl(QtCore.QUrl(url))
            self.setCentralWidget(self.web_view)
    
    
    if __name__ == "__main__":
        web_url = 'https://bokeh.pydata.org/en/latest/'
        if len(sys.argv) == 2:
            web_url = sys.argv[1]
        app = QtWidgets.QApplication(sys.argv)
        window = WebViewWindow(web_url)
        window.show()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
