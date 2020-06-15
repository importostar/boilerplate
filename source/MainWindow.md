---
title: MainWindow
date: 2020-05-07
---
Example Python program MainWindow.py

## Modules

* from PyQt5 import QtCore, QtWidgets
* from PyQt5.QtWidgets import QWidget, QSplitter
* from PyQt5.QtWidgets import QLabel
* from PyQt5.QtWidgets import QCheckBox
* from PyQt5.QtWidgets import QGroupBox
* from PyQt5.QtWidgets import QScrollArea
* from PyQt5.QtWidgets import QHBoxLayout, QVBoxLayout, QGridLayout
* from PyQt5.QtCore import Qt

## Classes

* class MainWindow(QtWidgets.QMainWindow):

## Methods

* def __init__(self):
* def createLayout_group(self, number):
* def createLayout_Containers(self):
* def createLayout_SideBarWidgets(self):
* def createLayout_MainAreaWidgets(self):
* def initUI(self):
* def resizeEvent(self, event):
* def resize_mainContainer(self):

## Code

Example Python PyQt program :

    #!/usr/bin/python
    # -*- coding: utf-8 -*-
    from PyQt5 import QtCore, QtWidgets
    from PyQt5.QtWidgets import QWidget, QSplitter
    from PyQt5.QtWidgets import QLabel
    from PyQt5.QtWidgets import QCheckBox
    from PyQt5.QtWidgets import QGroupBox
    from PyQt5.QtWidgets import QScrollArea
    from PyQt5.QtWidgets import QHBoxLayout, QVBoxLayout, QGridLayout
    from PyQt5.QtCore import Qt
    
    
    lst = [u"Daldfadkfal lak jačl kačldfka jčldfkajsčdlfkajsdčflajsdlčfk ajsdf", u"E", u"EF", u"F", u"FG", u"G", u"H", u"JS", u"J", u"K", u"M", u"P", u"R", u"S", u"T", u"U", u"V", u"X", u"Y", u"Z"]
    
    
    class MainWindow(QtWidgets.QMainWindow):
        resized = QtCore.pyqtSignal()
    
        def __init__(self):
            super(MainWindow, self).__init__()
    
            self.qs_mainContainer = QSplitter(Qt.Horizontal, self)
            self.qsa_sideBar = QScrollArea()
            self.qsa_mainArea = QScrollArea()
            self.w_helperForSideBar = QWidget()
            self.w_helperForMainArea = QWidget()
            self.qsa_sideBar.setWidget(self.w_helperForSideBar)
            self.qsa_mainArea.setWidget(self.w_helperForMainArea)
            self.vbl_sideBar = QVBoxLayout(self.w_helperForSideBar)
            self.vbl_mainArea = QVBoxLayout(self.w_helperForMainArea)
            self.window_width = 1024
            self.window_height = 768
            self.resize(self.window_width, self.window_height)
    
            self.initUI()
            # https://stackoverflow.com/questions/43126721/detect-resizing-in-widget-window-resized-signal/43126946#43126946
            self.resized.connect(self.resize_mainContainer)
    
        def createLayout_group(self, number):
            sgroupbox = QGroupBox("Group{}:".format(number), self)
            layout_groupbox = QVBoxLayout(sgroupbox)
            for i in range(len(lst)):
                item = QCheckBox(lst[i], sgroupbox)
                layout_groupbox.addWidget(item)
            layout_groupbox.addStretch(1)
            return sgroupbox
    
        def createLayout_Containers(self):
            self.qs_mainContainer.setMinimumHeight(self.frameGeometry().height())
            self.qs_mainContainer.setMinimumWidth(self.frameGeometry().width())
            self.qs_mainContainer.setHandleWidth(1)
            self.qs_mainContainer.setStretchFactor(4, 0)
            self.qs_mainContainer.setStretchFactor(1, 1)
            self.qs_mainContainer.addWidget(self.qsa_sideBar)
            self.qs_mainContainer.addWidget(self.qsa_mainArea)
    
            self.qsa_sideBar.minimumWidth()
            self.qsa_sideBar.setWidgetResizable(True)
            self.qsa_mainArea.setWidgetResizable(True)
    
            for i in range(1):
                self.vbl_sideBar.addWidget(self.createLayout_group(i))
            self.vbl_sideBar.addStretch(1)
    
            for i in range(2):
                self.vbl_mainArea.addWidget(self.createLayout_group(i))
            self.vbl_mainArea.addStretch(1)
    
        def createLayout_SideBarWidgets(self):
            pass
    
        def createLayout_MainAreaWidgets(self):
            pass
    
        def initUI(self):
            self.createLayout_Containers()
            self.show()
    
        def resizeEvent(self, event):
            self.resized.emit()
            return super(QtWidgets.QMainWindow, self).resizeEvent(event)
    
        def resize_mainContainer(self):
            # for size increment
            self.qs_mainContainer.setMinimumSize(self.frameGeometry().width(), self.frameGeometry().height())
            # for size decrement
            self.qs_mainContainer.setMaximumSize(self.frameGeometry().width(), self.frameGeometry().height())
            self.qsa_sideBar.setHorizontalScrollBarPolicy(QtCore.Qt.ScrollBarAsNeeded)
            self.qsa_sideBar.setVerticalScrollBarPolicy(QtCore.Qt.ScrollBarAsNeeded)
            self.qsa_mainArea.setHorizontalScrollBarPolicy(QtCore.Qt.ScrollBarAsNeeded)
            self.qsa_mainArea.setVerticalScrollBarPolicy(QtCore.Qt.ScrollBarAsNeeded)
        

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
