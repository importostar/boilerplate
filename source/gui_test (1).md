---
title: gui_test (1)
date: 2020-05-07
---
Example Python program gui_test (1).py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5.QtWidgets import QApplication, QMenuBar, QTreeView, \
* from PyQt5.QtGui import QStandardItem, QStandardItemModel, QIcon
* from PyQt5.QtCore import QSize, Qt
* import sys

## Classes

* class QCustomItem(QStandardItem):
* class FileTree(QTreeView):
* class main(QWidget):

## Methods

* def getIcon(iconType):
* def __init__(self, text, data_type=-1):
* def setType(self, data_type):
* def __init__(self):
* def initUI(self):
* def isCollapsed(self, index):
* def isExpanded(self, index):
* def __init__(self):
* def initUI(self):
* def getIcon(iconType):

## Code

Example Python PyQt program :

    from PyQt5.QtWidgets import QApplication, QMenuBar, QTreeView, \
          QHBoxLayout, QVBoxLayout, QWidget, QStyle, qApp, QFrame, \
          QAction, QMenu
    from PyQt5.QtGui import QStandardItem, QStandardItemModel, QIcon
    from PyQt5.QtCore import QSize, Qt
    import sys
    
    def getIcon(iconType):
        if   iconType == 21:
            return qApp.style().standardIcon(QStyle.SP_DirOpenIcon)
        elif iconType == 22:
            return qApp.style().standardIcon(QStyle.SP_DirClosedIcon)
        elif iconType == 42:
            return qApp.style().standardIcon(QStyle.SP_DialogOpenButton)
        elif iconType == 56:
            return qApp.style().standardIcon(QStyle.SP_DirHomeIcon)
    
    class QCustomItem(QStandardItem):
        def __init__(self, text, data_type=-1):
            super().__init__(text)
            self.type = data_type
    
        def setType(self, data_type):
            self.type = data_type
    
    class FileTree(QTreeView):
        def __init__(self):
            super().__init__()
            self.initUI()
    
        def initUI(self):
            self.setMaximumSize(QSize(500, 4000))
            model = QStandardItemModel()
            self.setModel(model)
            parent1 = QCustomItem("Root", data_type=1)
            #parent1.setIcon(getIcon(56))
            model.appendRow(parent1)
            child1 = QStandardItem("")
            child1.setSelectable(0)
            parent1.appendRow([child1])
            '''for i in [21, 22]:
                parent1 = QCustomItem("Null Node", data_type=1)
                for j in range(3):
                    child1 = QStandardItem('Child {}'.format(i*3+j))
                    child2 = QStandardItem('row: {}, col: {}'.format(i, j+1))
                    child3 = QStandardItem('row: {}, col: {}'.format(i, j+2))
                    parent1.appendRow([child1, child2, child3])
                parent1.setIcon(getIcon(i))
                model.appendRow(parent1)
                # span container columns
                self.setFirstColumnSpanned(i, self.rootIndex(), True)'''
            self.collapsed.connect(self.isCollapsed)
            self.expanded.connect(self.isExpanded)
            self.setHeaderHidden(True)
    
        def isCollapsed(self, index):
            print(index.row())
            
        def isExpanded(self, index):
            print(index.row())
            
        
    
    class main(QWidget):
        def __init__(self):
            super().__init__()
            self.initUI()
    
        def initUI(self):
            window = QVBoxLayout()
            window.setContentsMargins(0, 0, 0, 0)
            self.setLayout(window)
            menu = QMenuBar()
            file = QMenu("&File", menu)
            menu.addMenu(file)
            openButton = QAction("&Open", file)
            file.addAction(openButton)
            window.addWidget(menu)
            
            layout = QHBoxLayout()
            layout.addWidget(FileTree())
            frame = QFrame()
            frame.setStyleSheet("background-color: #E5E5E5;border: 1px solid #828790")
            layout.addWidget(frame)
            layout.setContentsMargins(11, 0, 11, 11)
            window.addLayout(layout)
    
            self.setGeometry(300, 300, 800, 300) #screen x, y, window w, h
            self.setWindowTitle("Nintendo Editor v0.1 Alpha")
            self.show()
            
    
    if __name__ == "__main__":
        app = QApplication(sys.argv)
        ex = main()
        sys.exit(app.exec_())
    
    '''
    def getIcon(iconType):
        if   iconType == 0:
            return qApp.style().standardIcon(QStyle.SP_TitleBarMenuButton)
        elif iconType == 1:
            return qApp.style().standardIcon(QStyle.SP_TitleBarMinButton)
        elif iconType == 2:
            return qApp.style().standardIcon(QStyle.SP_TitleBarMaxButton)
        elif iconType == 3:
            return qApp.style().standardIcon(QStyle.SP_TitleBarCloseButton)
        elif iconType == 4:
            return qApp.style().standardIcon(QStyle.SP_TitleBarNormalButton)
        elif iconType == 5:
            return qApp.style().standardIcon(QStyle.SP_TitleBarShadeButton)
        elif iconType == 6:
            return qApp.style().standardIcon(QStyle.SP_TitleBarUnshadeButton)
        elif iconType == 7:
            return qApp.style().standardIcon(QStyle.SP_TitleBarContextHelpButton)
        elif iconType == 8:
            return qApp.style().standardIcon(QStyle.SP_DockWidgetCloseButton)
        elif iconType == 9:
            return qApp.style().standardIcon(QStyle.SP_MessageBoxInformation)
        elif iconType == 10:
            return qApp.style().standardIcon(QStyle.SP_MessageBoxWarning)
        elif iconType == 11:
            return qApp.style().standardIcon(QStyle.SP_MessageBoxCritical)
        elif iconType == 12:
            return qApp.style().standardIcon(QStyle.SP_MessageBoxQuestion)
        elif iconType == 13:
            return qApp.style().standardIcon(QStyle.SP_DesktopIcon)
        elif iconType == 14:
            return qApp.style().standardIcon(QStyle.SP_TrashIcon)
        elif iconType == 15:
            return qApp.style().standardIcon(QStyle.SP_ComputerIcon)
        elif iconType == 16:
            return qApp.style().standardIcon(QStyle.SP_DriveFDIcon)
        elif iconType == 17:
            return qApp.style().standardIcon(QStyle.SP_DriveHDIcon)
        elif iconType == 18:
            return qApp.style().standardIcon(QStyle.SP_DriveCDIcon)
        elif iconType == 19:
            return qApp.style().standardIcon(QStyle.SP_DriveDVDIcon)
        elif iconType == 20:
            return qApp.style().standardIcon(QStyle.SP_DriveNetIcon)
        elif iconType == 21:
            return qApp.style().standardIcon(QStyle.SP_DirOpenIcon)
        elif iconType == 22:
            return qApp.style().standardIcon(QStyle.SP_DirClosedIcon)
        elif iconType == 23:
            return qApp.style().standardIcon(QStyle.SP_DirLinkIcon)
        elif iconType == 24:
            return qApp.style().standardIcon(QStyle.SP_DirLinkOpenIcon)
        elif iconType == 25:
            return qApp.style().standardIcon(QStyle.SP_FileIcon)
        elif iconType == 26:
            return qApp.style().standardIcon(QStyle.SP_FileLinkIcon)
        elif iconType == 27:
            return qApp.style().standardIcon(QStyle.SP_ToolBarHorizontalExtensionButton)
        elif iconType == 28:
            return qApp.style().standardIcon(QStyle.SP_ToolBarVerticalExtensionButton)
        elif iconType == 29:
            return qApp.style().standardIcon(QStyle.SP_FileDialogStart)
        elif iconType == 30:
            return qApp.style().standardIcon(QStyle.SP_FileDialogEnd)
        elif iconType == 31:
            return qApp.style().standardIcon(QStyle.SP_FileDialogToParent)
        elif iconType == 32:
            return qApp.style().standardIcon(QStyle.SP_FileDialogNewFolder)
        elif iconType == 33:
            return qApp.style().standardIcon(QStyle.SP_FileDialogDetailedView)
        elif iconType == 34:
            return qApp.style().standardIcon(QStyle.SP_FileDialogInfoView)
        elif iconType == 35:
            return qApp.style().standardIcon(QStyle.SP_FileDialogContentsView)
        elif iconType == 36:
            return qApp.style().standardIcon(QStyle.SP_FileDialogListView)
        elif iconType == 37:
            return qApp.style().standardIcon(QStyle.SP_FileDialogBack)
        elif iconType == 38:
            return qApp.style().standardIcon(QStyle.SP_DirIcon)
        elif iconType == 39:
            return qApp.style().standardIcon(QStyle.SP_DialogOkButton)
        elif iconType == 40:
            return qApp.style().standardIcon(QStyle.SP_DialogCancelButton)
        elif iconType == 41:
            return qApp.style().standardIcon(QStyle.SP_DialogHelpButton)
        elif iconType == 42:
            return qApp.style().standardIcon(QStyle.SP_DialogOpenButton)
        elif iconType == 43:
            return qApp.style().standardIcon(QStyle.SP_DialogSaveButton)
        elif iconType == 44:
            return qApp.style().standardIcon(QStyle.SP_DialogCloseButton)
        elif iconType == 45:
            return qApp.style().standardIcon(QStyle.SP_DialogApplyButton)
        elif iconType == 46:
            return qApp.style().standardIcon(QStyle.SP_DialogResetButton)
        elif iconType == 47:
            return qApp.style().standardIcon(QStyle.SP_DialogDiscardButton)
        elif iconType == 48:
            return qApp.style().standardIcon(QStyle.SP_DialogYesButton)
        elif iconType == 49:
            return qApp.style().standardIcon(QStyle.SP_DialogNoButton)
        elif iconType == 50:
            return qApp.style().standardIcon(QStyle.SP_ArrowUp)
        elif iconType == 51:
            return qApp.style().standardIcon(QStyle.SP_ArrowDown)
        elif iconType == 52:
            return qApp.style().standardIcon(QStyle.SP_ArrowLeft)
        elif iconType == 53:
            return qApp.style().standardIcon(QStyle.SP_ArrowRight)
        elif iconType == 54:
            return qApp.style().standardIcon(QStyle.SP_ArrowBack)
        elif iconType == 55:
            return qApp.style().standardIcon(QStyle.SP_ArrowForward)
        elif iconType == 56:
            return qApp.style().standardIcon(QStyle.SP_DirHomeIcon)
        elif iconType == 57:
            return qApp.style().standardIcon(QStyle.SP_CommandLink)
        elif iconType == 58:
            return qApp.style().standardIcon(QStyle.SP_VistaShield)
        elif iconType == 59:
            return qApp.style().standardIcon(QStyle.SP_BrowserReload)
        elif iconType == 60:
            return qApp.style().standardIcon(QStyle.SP_BrowserStop)
        elif iconType == 61:
            return qApp.style().standardIcon(QStyle.SP_MediaPlay)
        elif iconType == 62:
            return qApp.style().standardIcon(QStyle.SP_MediaStop)
        elif iconType == 63:
            return qApp.style().standardIcon(QStyle.SP_MediaPause)
        elif iconType == 64:
            return qApp.style().standardIcon(QStyle.SP_MediaSkipForward)
        elif iconType == 65:
            return qApp.style().standardIcon(QStyle.SP_MediaSkipBackward)
        elif iconType == 66:
            return qApp.style().standardIcon(QStyle.SP_MediaSeekForward)
        elif iconType == 67:
            return qApp.style().standardIcon(QStyle.SP_MediaSeekBackward)
        elif iconType == 68:
            return qApp.style().standardIcon(QStyle.SP_MediaVolume)
        elif iconType == 69:
            return qApp.style().standardIcon(QStyle.SP_MediaVolumeMuted)
        elif iconType == 70:
            return qApp.style().standardIcon(QStyle.SP_LineEditClearButton)'''
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
