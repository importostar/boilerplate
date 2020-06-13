---
title: createApp_cxfreeze
date: 2020-05-07
---
Example Python program createApp_cxfreeze.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5.QtCore import (QFile, pyqtSignal, Qt, QMimeData, QProcess, QObject, QEvent)
* from PyQt5.QtGui import QIcon
* from PyQt5.QtWidgets import (QApplication, QFileDialog, QMainWindow, QCheckBox, 
* from distutils.spawn import find_executable
* import encodings
* import sys
* mytext = """from cx_Freeze import setup, Executable, build
* import sys

## Classes

* class QLineEditDropHandler(QObject):
* class MainWindow(QMainWindow):

## Methods

* def __init__(self, parent=None):
* def eventFilter(self, obj, event):
* def __init__(self):
* def check_cxfreeze(self, name):
* def dragEnterEvent(self, event):
* def openInFile(self):
* def openOutFolder(self):
* def shell_started(self):
* def shell_ended(self):
* def createSetup(self):
* def createStatusBar(self):
* def msgbox(self, message):
* def myStyleSheet(self):

## Code

Example Python PyQt program :

    #!/usr/bin/python3
    # -*- coding: utf-8 -*-
    #############################################################################
    from PyQt5.QtCore import (QFile, pyqtSignal, Qt, QMimeData, QProcess, QObject, QEvent)
    from PyQt5.QtGui import QIcon
    from PyQt5.QtWidgets import (QApplication, QFileDialog, QMainWindow, QCheckBox, 
                QMessageBox, QHBoxLayout, QVBoxLayout, QWidget, QLabel, QMessageBox, QToolButton, QLineEdit)
    from distutils.spawn import find_executable
    import encodings
    import sys
    
    class QLineEditDropHandler(QObject):
    
        def __init__(self, parent=None):
            QObject.__init__(self, parent)
    
        def eventFilter(self, obj, event):
            text = obj.text()
            quote = str(chr(34))
            comma = str(chr(44))
            if event.type() == QEvent.DragEnter:
                event.accept()
            if event.type() == QEvent.Drop:
                md = event.mimeData()
                if md.hasUrls():
                    for url in md.urls():
                        if text != "":
                            obj.setText(text + comma  + quote + url.path()+ quote)
                        else:
                            obj.setText(quote + url.path()+ quote)
                        break
                event.accept()
            return QObject.eventFilter(self, obj, event)
    
    quote = str(chr(34))
    squote = str(chr(39))
    class MainWindow(QMainWindow):
        changed = pyqtSignal(QMimeData)
        def __init__(self):
            super(MainWindow, self).__init__()
            btnwidth = 150
            self.InFile = ''
            self.OutFolder = '/tmp'
            self.cmd = ''
            self.appname = ''
            self.process = QProcess()
            self.process.started.connect(self.shell_started)
            self.process.finished.connect(self.shell_ended)
    
            self.open_process = QProcess()
    
    #        self.setAcceptDrops(True)
            self.createStatusBar()
    
            self.setGeometry(0, 0, 600, 300)
            self.setFixedSize(600, 300)
            self.setStyleSheet(myStyleSheet(self))
            self.setWindowIcon(QIcon.fromTheme("gnome-mime-text-x-python"))
            #### path
            btnInPath = QToolButton()
            btnInPath.setToolButtonStyle(Qt.ToolButtonTextBesideIcon)
            btnInPath.setIcon(QIcon.fromTheme("gtk-open"))
            btnInPath.setText("select Python File")
            btnInPath.setFixedWidth(btnwidth)
            btnInPath.clicked.connect(self.openInFile)
            self.lblInPath = QLabel(self.InFile)
    
            hlayout = QHBoxLayout()
            hlayout.addWidget(btnInPath)
            hlayout.addWidget(self.lblInPath)
    
            #### output path
            btnOutPath = QToolButton()
            btnOutPath.setIcon(QIcon.fromTheme("gtk-open"))
            btnOutPath.setToolButtonStyle(Qt.ToolButtonTextBesideIcon)
            btnOutPath.setText("select Output Folder")
            btnOutPath.setFixedWidth(btnwidth)
            btnOutPath.clicked.connect(self.openOutFolder)
            self.lblOutPath = QLabel(self.OutFolder)
    
            hlayout2 = QHBoxLayout()
            hlayout2.addWidget(btnOutPath)
            hlayout2.addWidget(self.lblOutPath)
    
            #cmdlbl = QLabel("")
            createButton = QToolButton()
            createButton.setIcon(QIcon.fromTheme("gnome-mime-text-x-python"))
            createButton.setToolButtonStyle(Qt.ToolButtonTextBesideIcon)
            createButton.setText("create App")
            createButton.clicked.connect(self.createSetup)
            createButton.setFixedWidth(btnwidth)
    
            self.check3 = QCheckBox("use python3")
            self.check3.setToolTip("swith python2 / python3")
    
            self.exclude = QLineEdit(quote + "PyQt4" + quote + "," + quote + "matplotlib" + quote)
            self.exclude.setPlaceholderText("insert Modules (comma seperated in quotes)")
            self.exclude.setToolTip("insert Modules (comma seperated in quotes)")
            self.exclude.setAcceptDrops(True)
    
            self.include = QLineEdit()
            self.include.setPlaceholderText("insert Modules (comma seperated in quotes)")
            self.include.setToolTip("insert Modules (comma seperated in quotes in quotes)")
    
            self.include_files = QLineEdit()
            self.include_files.setPlaceholderText("insert file paths (comma seperated in quotes) or drop file here")
            self.include_files.setToolTip("insert file paths (comma seperated in quotes) or drop file here")
            self.include_files.setAcceptDrops(True)
            self.include_files.installEventFilter(QLineEditDropHandler(self))
    
            lbl1 = QLabel("include modules:")
            lbl2 = QLabel("exclude modules:")
            lbl3 = QLabel("include files:")
    
            vlayout = QVBoxLayout()
            vlayout.addLayout(hlayout)
            vlayout.addLayout(hlayout2)
            vlayout.addWidget(lbl1)
            vlayout.addWidget(self.include)
            vlayout.addWidget(lbl2)
            vlayout.addWidget(self.exclude)
            vlayout.addWidget(lbl3)
            vlayout.addWidget(self.include_files)
            vlayout.addWidget(self.check3)
            vlayout.addWidget(createButton)
    
            mywidget = QWidget()
            mywidget.setLayout(vlayout)
    
            self.setCentralWidget(mywidget)
    
            self.setWindowTitle("create App with cxfreeze")
    
        def check_cxfreeze(self, name):
            out = find_executable('cxfreeze')
            if out == None:
                return False
            else:
                return True
    
        def dragEnterEvent(self, event):
            self.statusBar().showMessage("File drop")
            event.acceptProposedAction()
            self.changed.emit(event.mimeData())
    
        def openInFile(self):
            fileName,_ = QFileDialog.getOpenFileName(self, "", "",  "Python Files (*.py)")
            if fileName:
                self.lblInPath.setText(fileName)
                self.InFile = fileName
                name = self.lblInPath.text().partition(".py")[0]
                name = name.rpartition("/")[-1]
                self.appname = name
                if self.OutFolder == "/tmp":
                    self.lblOutPath.setText(self.lblOutPath.text() + "/" + name)
                    self.OutFolder = self.lblOutPath.text()
    
        def openOutFolder(self):
            dlg = QFileDialog()
            dlg.setFileMode(QFileDialog.Directory)
            fileName = dlg.getExistingDirectory()
            if fileName:
                name = self.lblInPath.text().partition(".py")[0]
                name = name.rpartition("/")[-1]
                self.appname = name
                name = fileName + "/" + name
                self.lblOutPath.setText(name)
                self.OutFolder = name
    
        def shell_started(self):
            print("creating '" + self.appname)
            self.statusBar().showMessage("creating '" + self.appname + squote, 0)
    
        def shell_ended(self):
            print("'" + self.appname + "' created!")
            self.statusBar().showMessage("'" + self.appname + "' created!", 0)
            self.open_process.start("xdg-open", [self.OutFolder])
    
        def createSetup(self):
            mytext = """from cx_Freeze import setup, Executable, build
    import sys
    base = None
    if sys.platform == "win32":
        base = "Win32GUI"
    myname = self.appname
    desc = self.appname
    vers = "1.4"
    executables = [Executable(self.infile, base=base, targetName=self.appname)]
    
    build_exe_options = {"packages": ["idna"],
                                         "include_files": [my_include_files],
                                         "excludes": [my_excludes],
                                         "includes": [my_includes],
                                        "optimize": 2,
                                        "build_exe": self.OutFolder,
                                        }
    
    setup(
        name = self.appname,
        options = {"build_exe": build_exe_options},
        version = vers,
        description = desc,
        executables = executables
    )"""
            quote = str(chr(34))
            my_excludes = self.exclude.text()
            print("excluded modules: " + my_excludes)
            my_includes = self.include.text()
            print("included modules: " + my_includes)
            my_include_files = self.include_files.text()
            print("included files: " + my_includes)
    
            mytext = (mytext.replace("self.OutFolder",quote + self.OutFolder + quote).replace("self.appname", quote + self.appname + quote).replace("self.infile", quote + self.InFile + quote).replace("my_includes", my_includes).replace("my_excludes", my_excludes)).replace("my_include_files", my_include_files)
    
            f = "/tmp/mysetup.py"
            textfile = open(f, 'w')
            textfile.write(mytext)
            textfile.close()
            print(self.check3.isChecked())
            if self.check3.isChecked() == True:
                self.process.start("python3", ["/tmp/mysetup.py", "build"])
            else:
                self.process.start("python", ["/tmp/mysetup.py", "build"])
           
        def createStatusBar(self):
            self.statusBar().showMessage("Ready")
    
        def msgbox(self, message):
            QMessageBox.warning(self, "Message", message)
    
    def myStyleSheet(self):
        return """
    QToolButton
    {
    font-size: 9pt;
    color: #2e3436;
    }
    QLabel
    {
    font-weight: bold;
    font-size: 8pt;
    color: #204a87;
    }
    QStatusBar
    {
    font-size: 8pt;
    color: #3465a4;
    }
    QMainWindow
    {
    background: #f3f3f3;
    }
    QToolButton::hover
    {
    background: #babdb6;
    }
        """    
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        mainWin = MainWindow()
        mainWin.show()
        if mainWin.check_cxfreeze("cxfreeze") == False:
            QMessageBox.warning(mainWin, "Error", "<b>cxfreeze not found</b><br><br><i>Please install cxfreeze</i>")
            quit()
        else:
            mainWin.statusBar().showMessage("Ready * found cxfreeze", 0)
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
