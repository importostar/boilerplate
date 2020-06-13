---
title: teste
date: 2020-05-07
---
Example Python program teste.py
This program creates a PyQt GUI

## Modules

* import os
* import sys
* from PyQt5.QtWidgets import QApplication
* from PyQt5.QtWebKitWidgets import QWebView
* from PyQt5.QtGui import QIcon
* from PyQt5.QtCore import QUrl
* from PyQt5.QtCore import QSize
* from PyQt5.QtWebKit import QWebSettings
* from directory.filename import PyFileClass

## Code

Example Python PyQt program :

    #!/usr/bin/python3
    # -*- coding: utf-8 -*-
    
    import os
    import sys
    from PyQt5.QtWidgets import QApplication
    from PyQt5.QtWebKitWidgets import QWebView
    from PyQt5.QtGui import QIcon
    from PyQt5.QtCore import QUrl
    from PyQt5.QtCore import QSize
    
    if __name__ == "__main__":
    
        # Create application
        app = QApplication([])
    	
        # Create View
        web = QWebView()
    
        # Set Title
        web.setWindowTitle("My Application")
    
        # Set icon
        icon = QIcon()
        icon.addFile(":/my-icon.png", QSize(32,32))
        web.setWindowIcon(icon)
    
        # Define geometry
        width, height = 800, 600
        web.resize(width, height)
        
        # Define Position
        x = y = None
        if(x is None or y is None):
            web.move(app.desktop().screen().rect().center() - web.rect().center()) # center
        else:
            web.move(int(x), int(y))
    	
        # Show Debug
        debug = False 
        if debug:
            # Enable extra tools for developers
            from PyQt5.QtWebKit import QWebSettings
            web.page().settings().setAttribute(QWebSettings.DeveloperExtrasEnabled, True)
    
    
        # Html
        html = QUrl("file://" + os.getcwd() + "/index.html")
        web.load(html)
        
        # Load Pyjs File from 
        from directory.filename import PyFileClass
        PyFileClass = PyFileClass()
        web.page().mainFrame().addToJavaScriptWindowObject("PyFileClass", PyFileclass)
    
        # Show webview
        web.show()
    
        # Quit application
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
