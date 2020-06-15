---
title: PTBrowserFusion (1)
date: 2020-05-07
---
Example Python program PTBrowserFusion (1).py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5.QtWidgets import QApplication, QMainWindow, QWidget, QListWidget
* from PyQt5.QtWidgets import QHBoxLayout, QVBoxLayout, QTextEdit, QPushButton, QPlainTextEdit
* from PyQt5 import QtGui, QtCore
* import os, sys
* import json, re

## Classes

* class MainWindow(QMainWindow):

## Methods

* def is_target_folder(sub_path):
* def collect_path(sub_path, depth):
* def glob_folders(top_path):
* def __init__(self, data, parent=None):
* def on_search(self):
* def item_double_click(self, index):
* def prepare_data():

## Code

Example Python PyQt program :

    from PyQt5.QtWidgets import QApplication, QMainWindow, QWidget, QListWidget
    from PyQt5.QtWidgets import QHBoxLayout, QVBoxLayout, QTextEdit, QPushButton, QPlainTextEdit
    from PyQt5 import QtGui, QtCore
    
    # list all folder with depth 2 then save
    # gen app command : pyinstaller -F PTBrowserSimple.py
    
    import os, sys
    import json, re
    
    def is_target_folder(sub_path):
        return "col_" in sub_path or "fstore" in sub_path
    
    global_valid_entries = []
    def collect_path(sub_path, depth):
        res = []
        if depth <= 0:
            res.append(sub_path)
        else:
            for entry in os.scandir(sub_path):
                if os.access(entry, os.R_OK):
                    res += collect_path(entry.path, depth - 1)
        return res
    
    def glob_folders(top_path):
        if not os.access(top_path, os.R_OK):
            return
        for entry in os.scandir(top_path):
            if os.access(entry, os.R_OK) and is_target_folder(entry.path):
                global global_valid_entries
                global_valid_entries += collect_path(entry.path, 1)
    
    class MainWindow(QMainWindow):
        def __init__(self, data, parent=None):
            super(MainWindow, self).__init__(parent)
            self.data = data
            self.setWindowTitle('PTBrowser')
    
            toolbar = QHBoxLayout()
            search_text = QPlainTextEdit("regex-to-edit")
            search_text.setMaximumSize(400, 30)
            self.search_text = search_text
            search_btn = QPushButton("update")
            search_btn.pressed.connect(self.on_search)
    
            toolbar.addWidget(search_text)
            toolbar.addWidget(search_btn)
    
            path_list = QListWidget()
            path_list.addItems(global_valid_entries)
            path_list.doubleClicked.connect(self.item_double_click)
            self.path_list = path_list
    
            top_layout = QVBoxLayout()
            top_layout.addLayout(toolbar, 1)
            top_layout.addWidget(path_list, 10)
            widget = QWidget()
            widget.setLayout(top_layout)
            self.setCentralWidget(widget)
    
        def on_search(self):
            text = self.search_text.toPlainText()
            try:
                re_obj = re.compile(text)
            except Exception as e:
                print(e)
                return
    
            for idx in range(self.path_list.count()):
                item = self.path_list.item(idx)
                current = item.text()
                item.setHidden(not re_obj.search(current))
    
        def item_double_click(self, index):
            item = self.path_list.itemFromIndex(index)
            QtGui.QDesktopServices.openUrl(QtCore.QUrl.fromLocalFile(item.text()))
    
    
    
    def prepare_data():
        global global_valid_entries
        try:
            with open("data-cache.json", encoding="utf-8") as f:
                global_valid_entries = json.load(f.read())
        except Exception as e:
            pass
    
        if not global_valid_entries:
            for letter in 'GHIJKLMNOPQRSTUVWXYZ':
                glob_folders("{}:\\".format(letter))
    
            with open("data-cache.json", "w", encoding='utf-8') as jsonfile:
                json.dump(global_valid_entries, jsonfile, ensure_ascii=False)
    
        global_valid_entries.sort(key = lambda x : x[2:] if len(x) > 2 else "0")
    
    if __name__ == "__main__":
        prepare_data()
    
        app = QApplication(sys.argv)
        w = MainWindow(global_valid_entries)
        w.showMaximized()
    
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
