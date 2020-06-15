---
title: resize_issue
date: 2020-05-07
---
Example Python program resize_issue.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import argparse
* import functools
* import sys
* from PyQt5.QtCore import QObject, QEvent
* from PyQt5.QtWidgets import QApplication, QDialog, QVBoxLayout, QPushButton

## Classes

* class MyEventFilter(QObject):

## Methods

* def __init__(self, parent=None):
* def eventFilter(self, obj, event):
* def onClick(dialog, checked):
* def main():

## Code

Example Python PyQt program :

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    """
    Minimal reproduction program for the following issue:
    
    In sway WM, when the mouse cursor leaves a floating window, it sends a resize
    event to it, resizing it back to its previous size.
    
    Requirements:
    
    - Python 3 or Python 2 (latter untested)
    - PyQt5 (https://pypi.org/project/PyQt5/) for the Python version above
    - sway running
    - Environment variable QT_QPA_PLATFORM set to "wayland-egl"
    
    Steps to reproduce:
    
    1. Run: python resize_issue.py
    2. Make the window floating (if it isn't already)
    3. Click the button reading "Resize me"
    4. Observe the window being resized (as expected)
    5. Move the mouse cursor out of the window area
    6. Observe the window being resized to its old size (not expected)
    7. Observe the console output showing that the resize event is spontaneous, i.e.
       comes from the window system
    """
    
    import argparse
    import functools
    import sys
    
    from PyQt5.QtCore import QObject, QEvent
    from PyQt5.QtWidgets import QApplication, QDialog, QVBoxLayout, QPushButton
    
    
    class MyEventFilter(QObject):
    
        def __init__(self, parent=None):
            QObject.__init__(self, parent)
    
    
        def eventFilter(self, obj, event):
            if QEvent.Resize == event.type():
                print("resize: {}/{} -> {}/{} (spontaneous? {})".format \
                    ( event.oldSize().width()
                    , event.oldSize().height()
                    , event.size().width()
                    , event.size().height()
                    , event.spontaneous()
                    ))
    
            return QObject.eventFilter(self, obj, event)
    
    
    def onClick(dialog, checked):
        dialog.resize(400, 400)
    
    
    def main():
        app = QApplication(sys.argv)
    
        button = QPushButton("Resize me")
    
        layout = QVBoxLayout()
        layout.addWidget(button)
    
        dialog = QDialog()
        dialog.setLayout(layout)
        dialog.installEventFilter(MyEventFilter(dialog))
    
        button.clicked.connect(functools.partial(onClick, dialog))
    
        dialog.open()
    
        return app.exec_()
    
    
    if __name__ == "__main__":
        sys.exit(main())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
