---
title: pyqt5_app_template
date: 2020-05-07
---
Example Python program pyqt5_app_template.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5 import QtWidgets
* from PyQt5.QtWidgets import QAction
* from PyQt5.QtGui import QIcon, QKeySequence
* import sys
* from PyQt5.QtWidgets import QApplication

## Classes

* class MainWindow(QtWidgets.QMainWindow):

## Methods

* def __init__(self, *args, **kwargs):
* def closeEvent(self, event):
* def new(self):
* def open(self):
* def save(self):
* def saveas(self):
* def check_modified(self):
* def _create_actions(self):
* def _create_menus(self):
* def _create_toolbars(self):
* def dummy():
* def main():

## Code

Example Python PyQt program :

    #!/usr/bin/env python3
    
    from PyQt5 import QtWidgets
    from PyQt5.QtWidgets import QAction
    from PyQt5.QtGui import QIcon, QKeySequence
    
    
    class MainWindow(QtWidgets.QMainWindow):
    
        def __init__(self, *args, **kwargs):
            super().__init__(*args, **kwargs)
    
            self.tableview = QtWidgets.QTableWidget(self)
            self.setCentralWidget(self.tableview)
    
            self._create_actions()
            self._create_menus()
            self._create_toolbars()
            
        def closeEvent(self, event):
            """
            Override closeEvent to check for unsaved changes and
            to write application settings, if any.
            """
            if self.check_modified():
                # self.write_settings()
                event.accept()
            else:
                event.ignore()
    
        def new(self):
            print("new()")
    
        def open(self):
            print("open()")
    
        def save(self):
            print("save()")
    
        def saveas(self):
            print("saveas()")
    
        def check_modified(self):
            """
            If the environment has unsaved modifications, ask the user if
            they would like to save their changes before continuing.
            """
            ## possible code:
            # if self.is_modified:
            #   reply = QMessageBox.warning(self, "MyApplication",
            #       "Do you want to save your changes?",
            #       QMessageBox.Cancel|QMessageBox.Discard|QMessageBox.Save)
            #
            #   if reply == QMessageBox.Save:
            #       return self.save()
            #   if reply == QMessageBox.Cancel:
            #       return False
            # return True
            return True
    
        def _create_actions(self):
            qks=QKeySequence
            icon=QIcon().fromTheme
    
            ## main actions
    
            self.action_new = QAction(icon("document-new"),
                                      "&New", self,
                                      shortcut=qks.New,
                                      triggered=self.new)
    
            self.action_open = QAction(icon("document-open"),
                                       "&Open...", self,
                                       shortcut=qks.Open,
                                       triggered=self.open)
    
            self.action_save = QAction(icon("document-save"),
                                       "&Save", self,
                                       shortcut=qks.Save,
                                       triggered=self.save)
    
            self.action_saveas = QAction(icon("document-save-as"),
                                         "Save &As...", self,
                                         shortcut=qks.SaveAs,
                                         triggered=self.saveas)
    
            self.action_quit = QAction(icon("application-exit"),
                                       "&Quit", self,
                                       shortcut=qks.Quit,
                                       triggered=self.close)
    
            ## edit actions
            # these will usually be connected to methods of the editor
            # (e.g. the table widget, a text edit, etc.)
    
            self.action_copy = QAction(icon("edit-copy"),
                                       "&Copy", self,
                                       shortcut=qks.Copy,
                                       triggered=dummy)
    
            self.action_cut = QAction(icon("edit-cut"),
                                      "Cu&t", self,
                                      shortcut=qks.Cut,
                                      triggered=dummy)
    
            self.action_paste = QAction(icon("edit-paste"),
                                        "&Paste", self,
                                        shortcut=qks.Paste,
                                        triggered=dummy)
    
            ## disable some actions at application start;
            ## i.e. the ones that don't make sense without an open document
    
            for a in (self.action_save, self.action_saveas,
                      self.action_copy, self.action_cut, self.action_paste):
                a.setEnabled(False)
    
        def _create_menus(self):
            self.menu_file : QtWidgets.QMenu = self.menuBar().addMenu("&File")
            self.menu_edit : QtWidgets.QMenu = self.menuBar().addMenu("&Edit")
    
            self.menu_file.addAction(self.action_new)
            self.menu_file.addAction(self.action_open)
            self.menu_file.addAction(self.action_save)
            self.menu_file.addAction(self.action_saveas)
            self.menu_file.addSeparator()
            self.menu_file.addAction(self.action_quit)
    
            self.menu_edit.addAction(self.action_copy)
            self.menu_edit.addAction(self.action_cut)
            self.menu_edit.addAction(self.action_paste)
    
        def _create_toolbars(self):
            self.toolbar_file : QtWidgets.QToolBar = self.addToolBar("File")
            self.toolbar_edit : QtWidgets.QToolBar = self.addToolBar("Edit")
    
            self.toolbar_file.addAction(self.action_new)
            self.toolbar_file.addAction(self.action_open)
            self.toolbar_file.addAction(self.action_save)
    
            self.toolbar_edit.addAction(self.action_copy)
            self.toolbar_edit.addAction(self.action_cut)
            self.toolbar_edit.addAction(self.action_paste)
    
    def dummy():
        print("triggered")
    
    def main():
        import sys
        from PyQt5.QtWidgets import QApplication
    
        app=QApplication(sys.argv)
        mw=MainWindow()
        mw.show()
        sys.exit(app.exec_())
    
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
