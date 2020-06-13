---
title: rerenamer
date: 2020-05-07
---
Example Python program rerenamer.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os, sys
* from urllib.parse import unquote, urlsplit
* import fnmatch, re, sre_constants
* from PyQt5 import uic
* from PyQt5.QtCore import QObject, Qt
* from PyQt5.QtWidgets import (

## Classes

* class MainWindow(QMainWindow):

## Methods

* def __init__(self, files):
* def add_files(self):
* def load_ui(self):
* def find_replace(self, find, replace, is_regex, case_sensitive):
* def update_previews(self):
* def on_cancel(self, *args):
* def on_ok(self, *args):
* def on_preview(self, *args):

## Code

Example Python PyQt program :

    #!/usr/bin/python3
    
    import os, sys
    from urllib.parse import unquote, urlsplit
    import fnmatch, re, sre_constants
    
    from PyQt5 import uic
    from PyQt5.QtCore import QObject, Qt
    from PyQt5.QtWidgets import (
        QWidget, QApplication, QDesktopWidget,
        QHeaderView, QStyle, QTableWidgetItem, QMainWindow)
    
    
    
    class MainWindow(QMainWindow):
    
        def __init__(self, files):
            super().__init__()
            files = [unquote(urlsplit(f).path) for f in files]
            self.files = [f for f in files if os.path.exists(f)]
            self.new_files = {}
            self.load_ui()
            self.add_files()
            self.ui.show()
    
    
        def add_files(self):
            ui = self.ui
            flags = Qt.ItemFlags()
            flags &= Qt.ItemIsEnabled
            flags &= QStyle.State_Active
            flags &= QStyle.State_Enabled
    
            for i, f in enumerate(self.files):
                ui.preview_table.insertRow(i)
    
                item = QTableWidgetItem(os.path.basename(f))
                item.setFlags(flags)
                ui.preview_table.setItem(i, 0, item)
                ui.preview_table.setItem(i, 1, QTableWidgetItem(''))
    
    
        def load_ui(self):
            uifilename = __file__.replace('.py', '.ui')
            ui = uic.loadUi(uifilename)
    
            header = ui.preview_table.horizontalHeader()
            header.setSectionResizeMode(0, QHeaderView.Stretch)
            header.setSectionResizeMode(1, QHeaderView.Stretch)
    
            ui.find_text.textChanged.connect(self.on_preview)
            ui.replace_text.textChanged.connect(self.on_preview)
            ui.regex_checkbox.clicked.connect(self.on_preview)
            ui.case_checkbox.clicked.connect(self.on_preview)
            ui.okclose_buttonbox.accepted.connect(self.on_ok)
            ui.okclose_buttonbox.rejected.connect(self.on_cancel)
    
            rect = ui.frameGeometry()
            centre = QDesktopWidget().availableGeometry().center()
            rect.moveCenter(centre)
            ui.move(rect.topLeft())
    
            self.ui = ui
    
    
        def find_replace(self, find, replace, is_regex, case_sensitive):
            if not is_regex:
                find = fnmatch.translate(find).replace(r'\Z','')
    
            #todo regex error handling
            try:
                flags = 0
                if not case_sensitive:
                    flags = re.IGNORECASE
                regex = re.compile(find, flags)
            except sre_constants.error:
                return (None, None, None)
    
            for fp in self.files:
                f,e =  os.path.splitext(os.path.basename(fp))
                try:
                    f = regex.sub(replace, f)
                except sre_constants.error:
                    yield (None, None, None)
                fn = os.path.join(os.path.dirname(fp), f+e)
                yield (fp, fn, f+e)
    
    
        def update_previews(self):
            ui = self.ui
            self.new_files = {}
    
            find = ui.find_text.text()
            if not find:
                for i in range(len(self.files)):
                    ui.preview_table.setItem(i, 1, QtGui.QTableWidgetItem(''))
    
            replace = ui.replace_text.text()
            is_regex = ui.regex_checkbox.isChecked()
            case_sensitive = ui.case_checkbox.isChecked()
    
            for i, (fp, fn, fe) in enumerate(self.find_replace(find, replace, is_regex, case_sensitive)):
                print(repr((fp, fn, fe)))
                if fp is None or fp == fn:
                    # continue
                    ui.preview_table.setItem(i, 1, QTableWidgetItem(''))
    
                if fn and fn != fp and not os.path.exists(fn):
                    ui.preview_table.setItem(i, 1, QTableWidgetItem(fe))
                    self.new_files[fp] = fn
    
    
        def on_cancel(self, *args):
            self.ui.close()
    
    
        def on_ok(self, *args):
            for fp, fn in self.new_files.items():
                print(' '.join([fp, fn]))
                os.rename(fp, fn)
    
            self.ui.close()
    
    
        def on_preview(self, *args):
            self.update_previews()
    
    
    if __name__ == "__main__":
        try:
            files = sys.argv[1:]
        except:
            sys.exit(1)
    
        app = QApplication(sys.argv)
        mainwindow = MainWindow(files)
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
