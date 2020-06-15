---
title: Notepad
date: 2020-05-07
---
Example Python program Notepad.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtWidgets import QApplication,QAction,QMessageBox,QMainWindow,QMenuBar,QDialog,QTextEdit,QHBoxLayout,QFileDialog,QSlider,QFontComboBox,QVBoxLayout,QWidget,QFontDialog,QColorDialog,QFrame
* from PyQt5.QtGui import QIcon,QPainter,QPaintDevice,QTextFrame
* from PyQt5.QtCore import Qt,QRegularExpression,QDateTime
* from PyQt5.QtPrintSupport import QPrintDialog,QPrintPreviewWidget,QPrinter,QPrintPreviewDialog
* import cv2
* import numpy as np
* import sys,os
* from PIL  import ImageGrab

## Classes

* class window(QMainWindow):

## Methods

* def __init__(self):
* def MenuBar(self):
* def delete(self):
* def About(self):
* def setCurrentFileName(self, fileName=''):
* def maybeSave(self):
* def closeEvent(self, e):
* def PrinterPreview(self):
* def handlePaintRequest(self,printer):
* def Printer(self):
* def datetime(self):
* def Screencapture(self):
* def Exit(self):
* def Undo(self):
* def italic(self):
* def Redo(self):
* def Copy(self):
* def Cut(self):
* def Paste(self):
* def SelectALL(self):
* def Alignleft(self):
* def Alignright(self):
* def Aligncenter(self):
* def Underline(self):
* def Bold(self):
* def Newfile(self):
* def colorbox(self):
* def open(self):
* def save(self):
* def fontbox(self):

## Code

Example Python PyQt program :

    from PyQt5.QtWidgets import QApplication,QAction,QMessageBox,QMainWindow,QMenuBar,QDialog,QTextEdit,QHBoxLayout,QFileDialog,QSlider,QFontComboBox,QVBoxLayout,QWidget,QFontDialog,QColorDialog,QFrame
    from PyQt5.QtGui import QIcon,QPainter,QPaintDevice,QTextFrame
    from PyQt5.QtCore import Qt,QRegularExpression,QDateTime
    
    from PyQt5.QtPrintSupport import QPrintDialog,QPrintPreviewWidget,QPrinter,QPrintPreviewDialog
    import cv2
    import numpy as np
    
    import sys,os
    from PIL  import ImageGrab
    class window(QMainWindow):
        def __init__(self):
            super().__init__()
            self.setWindowTitle('Notepad')
            self.setWindowIcon(QIcon('icon.png'))
            self.setGeometry(0,20,1370,690)
            v_layout=QVBoxLayout()
    
    
    
            self.text=QTextEdit(self)
            self.text.setMouseTracking(True)
    
            self.setCurrentFileName()
            #self.text.setGeometry(0,20,1370,690)
            self.im=ImageGrab.grab()
            self.text.setLayout(v_layout)
            self.setCentralWidget(self.text)
            self.text.setFocus()
    
            self.show()
        def MenuBar(self):
            bar=self.menuBar()
            file=bar.addMenu('FILE')
            view=bar.addMenu('VIEW')
            Edit=bar.addMenu('EDIT')
            tools=bar.addMenu('TOOLS')
            help=bar.addMenu('HELP')
            screencap=QAction('Sceenshot',self)
            screencap.setShortcut("Ctrl+F9")
            screencap.setStatusTip('Screenshot')
            screencap.triggered.connect(self.Screencapture)
            tools.addAction(screencap)
    
    
    
            colorb = QAction('Color Box', self)
            colorb.setShortcut("Ctrl+F7")
            colorb.setStatusTip('Color Box')
            colorb.triggered.connect(self.colorbox)
            tools.addAction(colorb)
            fontb= QAction('Font Style', self)
            fontb.setShortcut('Ctrl+F8')
            fontb.setToolTip('Font Style')
            fontb.triggered.connect(self.fontbox)
            tools.addAction(fontb)
            newfile = QAction('New', self)
            newfile.setShortcut('Ctrl+N')
            newfile.setStatusTip('New File')
            newfile.triggered.connect(self.Newfile)
            file.addAction(newfile)
            Openfile = QAction('Open', self)
            Openfile.setShortcut('Ctrl+O')
            Openfile.setStatusTip('Open File')
            Openfile.triggered.connect(self.open)
            file.addAction(Openfile)
            savefile = QAction('Save As', self)
            savefile.setShortcut('Ctrl+S')
            savefile.setToolTip('Save As')
            savefile.triggered.connect(self.save)
            file.addAction(savefile)
    
            printfile = QAction('Print', self)
            printfile.setShortcut('Ctrl+P')
            printfile.setToolTip('Print')
            printfile.triggered.connect(self.Printer)
            file.addAction(printfile)
            printpreviewfile = QAction('Print Preview', self)
    
            printpreviewfile.setToolTip('Print Preview')
            printpreviewfile.triggered.connect(self.PrinterPreview)
            file.addAction(printpreviewfile)
    
            exitfile = QAction('Exit', self)
            exitfile.setShortcut('Ctrl+E')
            exitfile.setToolTip('Exit')
            exitfile.triggered.connect(self.Exit)
            file.addAction(exitfile)
    
            leftAlign = QAction('Left', self)
            leftAlign.setShortcut('Ctrl+F1')
            leftAlign.setToolTip('Align Left')
            leftAlign.triggered.connect(self.Alignleft)
            view.addAction(leftAlign)
            centerAlign = QAction('Center', self)
            centerAlign.setShortcut('Ctrl+F2')
            centerAlign.setToolTip('Align Center')
            centerAlign.triggered.connect(self.Aligncenter)
            view.addAction(centerAlign)
            rightAlign = QAction('Right', self)
            rightAlign.setShortcut('Ctrl+F3')
            rightAlign.setToolTip('Align Right')
    
            rightAlign.triggered.connect(self.Alignright)
    
            view.addAction(rightAlign)
    
    
            undofile= QAction('Undo', self)
            undofile.setShortcut('Ctrl+Z')
            undofile.setToolTip('Exit')
            undofile.triggered.connect(self.Undo)
            Edit.addAction(undofile)
            redofile = QAction('Redo', self)
            redofile.setShortcut('Ctrl+Y')
            redofile.setToolTip('Exit')
            redofile.triggered.connect(self.Redo)
            Edit.addAction(redofile)
            italicfile = QAction('Italic', self)
            italicfile.setShortcut('Ctrl+I')
            italicfile.setToolTip('Italic')
            italicfile.triggered.connect(self.italic)
            Edit.addAction(italicfile)
            boldfile = QAction('Bold', self)
            boldfile.setShortcut('Ctrl+B')
            boldfile.setToolTip('Bold')
            boldfile.triggered.connect(self.Bold)
            Edit.addAction(boldfile)
            underline = QAction('Underline', self)
            underline.setShortcut('Ctrl+U')
            underline.setToolTip('Under line')
            underline.triggered.connect(self.Underline)
    
            Edit.addAction(underline)
            copyfile = QAction(QIcon.fromTheme('edit-copy'),'Copy', self)
            copyfile.setShortcut('Ctrl+C')
            copyfile.setToolTip('Exit')
            copyfile.triggered.connect(self.Copy)
            Edit.addAction(copyfile)
            cutfile = QAction('Cut', self)
            cutfile.setShortcut('Ctrl+X')
            cutfile.setToolTip('Exit')
            cutfile.triggered.connect(self.Cut)
            Edit.addAction(cutfile)
            pastefile = QAction('Paste', self)
            pastefile.setShortcut('Ctrl+V')
            pastefile.setToolTip('Exit')
            pastefile.triggered.connect(self.Paste)
            Edit.addAction(pastefile)
    
            selectfile = QAction('Select ALL', self)
            selectfile.setShortcut('Ctrl+A')
            selectfile.setToolTip('Exit')
            selectfile.triggered.connect(self.SelectALL)
            Edit.addAction(selectfile)
            deletefile = QAction('Delete', self)
            deletefile.setShortcut('Ctrl+D')
            deletefile.setToolTip('Delete')
            deletefile.triggered.connect(self.delete)
            Edit.addAction(deletefile)
            date = QAction('Date Time', self)
            date.setShortcut('Ctrl+D')
            date.setToolTip('Date Time')
            date.triggered.connect(self.datetime)
            Edit.addAction(date)
    
            aboutfile = QAction(QIcon.fromTheme('about'),'About', self)
            aboutfile.setShortcut('Ctrl+F9')
            aboutfile.setToolTip('About')
            aboutfile.triggered.connect(self.About)
            help.addAction(aboutfile)
        def delete(self):
            cursor=self.text.textCursor()
            if not cursor.isNull():
                cursor.removeSelectedText()
    
        def About(self):
            msg = QMessageBox()
            msg.setIcon(QMessageBox.Information)
            msg.setText("Notepad")
            msg.setInformativeText("This is a Dektop Application.User can take Screenshot of his/her file ")
            msg.setWindowTitle("About")
            msg.setDetailedText("It is for all versions of Windows .It takes less Memory,It has a fabulous.For More information Goto Our website ")
            msg.setStandardButtons(QMessageBox.Ok | QMessageBox.Cancel)
    
            msg.exec_()
        def setCurrentFileName(self, fileName=''):
            self.fileName = fileName
            self.text.document().setModified(False)
    
            if not fileName:
                shownName = 'untitled.txt'
            else:
                shownName = QFileInfo(fileName).fileName()
    
            self.setWindowTitle(self.tr("%s[*] - %s" % (shownName, "Rich Text")))
            self.setWindowModified(False)
    
     
    
        
       
            
    
          
             
    
        def maybeSave(self):
            if not self.text.document().isModified():
                return True
    
            if self.fileName.startswith(':/'):
                return True
    
            ret = QMessageBox.warning(self, "Application",
                                      "The document has been modified.\n"
                                      "Do you want to save your changes?",
                                      QMessageBox.Save | QMessageBox.Discard | QMessageBox.Cancel)
    
            if ret == QMessageBox.Save:
                return self.save()
    
            if ret == QMessageBox.Cancel:
                return False
    
            return True
    
        def closeEvent(self, e):
            if self.maybeSave():
                e.accept()
            else:
                e.ignore()
        def PrinterPreview(self):
            dialog=QPrintPreviewDialog()
            dialog.paintRequested.connect(self.text.print_)
            dialog.exec_()
    
        def handlePaintRequest(self,printer):
            printer.setDocName(self.filename)
            document=self.text.document()
            document.print_(printer)
    
        def Printer(self):
            dialog=QPrintDialog()
            if(dialog.exec_()==QDialog.Accepted):
                self.text.document().print_(dialog.printer())
    
    
    
    
    
    
    
    
    
        def datetime(self):
            self.text.insertPlainText(QDateTime.currentDateTime().toString())
    
        def Screencapture(self):
            ImageGrab.grab().save('untitled.png')
        def Exit(self):
            sys.exit()
        def Undo(self):
            self.text.undo()
        def italic(self):
            self.text.setFontItalic(True)
    
        def Redo(self):
            self.text.redo()
    
        def Copy(self):
            self.text.copy()
    
        def Cut(self):
            self.text.cut()
    
        def Paste(self):
            self.text.paste()
        def SelectALL(self):
            self.text.selectAll()
        def Alignleft(self):
            self.text.setAlignment(Qt.AlignLeft)
        def Alignright(self):
            self.text.setAlignment(Qt.AlignJustify| Qt.AlignRight)
    
        def Aligncenter(self):
            self.text.setAlignment(Qt.AlignCenter)
    
        def Underline(self):
            self.text.setFontUnderline(True)
        def Bold(self):
            self.text.setFontPointSize(15)
        def Newfile(self):
            self.text.clear()
            self.setCurrentFileName()
        def colorbox(self):
            color=QColorDialog.getColor()
            if color.isValid():
                self.text.setTextColor(color)
    
        def open(self):
            filename=QFileDialog.getOpenFileName(self,'Open As',os.getenv('Home'))
            f=open(filename[0],'r')
            filetext=f.read()
            self.text.setText(filetext)
        def save(self):
            filename=QFileDialog.getSaveFileName(self,'Save As',os.getenv('Home'))
            f=open(filename[0],'w')
            mytext=self.text.toPlainText()
            f.write(mytext)
    
        def fontbox(self):
            font, ok = QFontDialog.getFont()
            if ok:
                self.text.setFont(font)
    
    
    
    app=QApplication(sys.argv)
    win=window()
    win.MenuBar()
    win.resize(400,400)
    sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
