---
title: test_mac_chained_dialogs
date: 2020-05-07
---
Example Python program test_mac_chained_dialogs.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5.QtCore import *
* from PyQt5.QtGui import *
* from PyQt5.QtWidgets import *

## Classes

* class MessageBoxMixin(object):
* class WindowModalDialog(QDialog, MessageBoxMixin):
* class MyDialog(WindowModalDialog):

## Methods

* def _(x): return x
* def top_level_window_recurse(self, window=None):
* def top_level_window(self):
* def question(self, msg, parent=None, title=None, icon=None):
* def show_warning(self, msg, parent=None, title=None):
* def show_error(self, msg, parent=None):
* def show_critical(self, msg, parent=None, title=None):
* def show_message(self, msg, parent=None, title=None):
* def msg_box(self, icon, parent, title, text, buttons=QMessageBox.Ok,
* def __init__(self, parent, title=None):
* def __init__(self, parent=None, title=None, ctr = 0):
* def spawn(self):
* def showEvent(self, e):

## Code

Example Python PyQt program :

    #!/usr/bin/env python3
    
    from PyQt5.QtCore import *
    from PyQt5.QtGui import *
    from PyQt5.QtWidgets import *
    
    def _(x): return x
    
    # taken from qt/util.py
    class MessageBoxMixin(object):
        def top_level_window_recurse(self, window=None):
            window = window or self
            classes = (WindowModalDialog, QMessageBox)
            for n, child in enumerate(window.children()):
                # Test for visibility as old closed dialogs may not be GC-ed
                if isinstance(child, classes) and child.isVisible():
                    return self.top_level_window_recurse(child)
            return window
    
        def top_level_window(self):
            return self.top_level_window_recurse()
    
        def question(self, msg, parent=None, title=None, icon=None):
            Yes, No = QMessageBox.Yes, QMessageBox.No
            return self.msg_box(icon or QMessageBox.Question,
                                parent, title or '',
                                msg, buttons=Yes|No, defaultButton=No) == Yes
    
        def show_warning(self, msg, parent=None, title=None):
            return self.msg_box(QMessageBox.Warning, parent,
                                title or _('Warning'), msg)
    
        def show_error(self, msg, parent=None):
            return self.msg_box(QMessageBox.Warning, parent,
                                _('Error'), msg)
    
        def show_critical(self, msg, parent=None, title=None):
            return self.msg_box(QMessageBox.Critical, parent,
                                title or _('Critical Error'), msg)
    
        def show_message(self, msg, parent=None, title=None):
            return self.msg_box(QMessageBox.Information, parent,
                                title or _('Information'), msg)
    
        def msg_box(self, icon, parent, title, text, buttons=QMessageBox.Ok,
                    defaultButton=QMessageBox.NoButton):
            parent = parent or self.top_level_window()
            d = QMessageBox(icon, title, str(text), buttons, parent)
            d.setWindowModality(Qt.WindowModal)
            d.setDefaultButton(defaultButton)
            return d.exec_()
    
    # taken from qt/util.py
    class WindowModalDialog(QDialog, MessageBoxMixin):
        '''Handy wrapper; window modal dialogs are better for our multi-window
        daemon model as other wallet windows can still be accessed.'''
        def __init__(self, parent, title=None):
            QDialog.__init__(self, parent)
            self.setWindowModality(Qt.WindowModal)
            if title:
                self.setWindowTitle(title)
    
    class MyDialog(WindowModalDialog):
    
        def __init__(self, parent=None, title=None, ctr = 0):
            super().__init__(parent=parent, title=title)
            self.timer = None
            self.ctr = ctr
            self.resize(320, 200)
            l = QVBoxLayout(self)
            l.addWidget(QLabel(str(title)))
            but = QPushButton()
            l.addWidget(but)
            but.setText("Close")
            but.clicked.connect(lambda x: self.close())
    
        def spawn(self):
            self.timer = QTimer(self); self.timer.setSingleShot(True)
            self.timer.timeout.connect(self.spawn)
            self.timer.start(1000)
            self.ctr += 1
            if self.ctr == 1:
                dlg = MyDialog(self, "Dialog 2", 2)
                dlg.show()
            elif self.ctr < 4:
                self.show_message("{} Message {}".format(self.windowTitle(), self.ctr))
    
        def showEvent(self, e):
            super().showEvent(e)
            self.spawn()
    
    
    if __name__ == "__main__":
        print(
            """
    Note: This script is used to illustrate an actual pathological situation on
    macOS. While it looks contrived, this situation happens with the Electron Cash
    'plugins' window. Behavior works as expected on Linux and on Windows.
    
    On macOS, after all the dialogs are done, you cannot interact with the base
    window anymore.
    
    Try hitting the Quit button on macOS after everything is dismissed. You can't.
    """)
        app = QApplication([])
        mainWin = QMainWindow(None)
        mainWin.resize(640, 480)
        but = QPushButton(mainWin)
        but.setText("Quit")
        but.clicked.connect(lambda x: app.quit())
        mainWin.show()
        dlg = MyDialog(mainWin, "Dialog 1")
        dlg.show()
        app.exec_()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
