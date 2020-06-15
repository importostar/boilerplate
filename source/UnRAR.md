---
title: UnRAR
date: 2020-05-07
---
Example Python program UnRAR.py
This program creates a PyQt GUI

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets
* import patoolib
* import sys
* import PyQt5.sip

## Classes

* class Ui_Frame(object):

## Methods

* def setupUi(self, Frame):
* def retranslateUi(self, Frame):
* def BrowseInput_Path(self):
* def BrowseOutput_Dir(self):
* def Extract(self):

## Code

Example Python PyQt program :

    from PyQt5 import QtCore, QtGui, QtWidgets
    import patoolib
    import sys
    import PyQt5.sip
    class Ui_Frame(object):
        def setupUi(self, Frame):
            self.Frame = Frame
            Frame.setObjectName("Frame")
            Frame.resize(489, 279)
            Frame.setStyleSheet("background-color: rgb(52, 101, 164);")
            Frame.setFrameShape(QtWidgets.QFrame.StyledPanel)
            Frame.setFrameShadow(QtWidgets.QFrame.Raised)
            self.gridLayout = QtWidgets.QGridLayout(Frame)
            self.gridLayout.setObjectName("gridLayout")
            self.txtoutput = QtWidgets.QLineEdit(Frame)
            self.txtoutput.setObjectName("txtoutput")
            self.gridLayout.addWidget(self.txtoutput, 2, 4, 1, 1)
            self.btninput = QtWidgets.QPushButton(Frame)
            self.btninput.setStyleSheet("background-color: rgb(233, 185, 110);")
            self.btninput.setObjectName("btninput")
    
            self.btninput.clicked.connect(self.BrowseInput_Path)
    
    
            self.gridLayout.addWidget(self.btninput, 0, 5, 1, 1)
            self.btnextract = QtWidgets.QPushButton(Frame)
            self.btnextract.setStyleSheet("background-color: rgb(173, 127, 168);")
            self.btnextract.setObjectName("btnextract")
            self.gridLayout.addWidget(self.btnextract, 4, 4, 1, 1)
    
            self.btnextract.clicked.connect(self.Extract)
    
    
            self.label = QtWidgets.QLabel(Frame)
            self.label.setLayoutDirection(QtCore.Qt.RightToLeft)
            self.label.setAlignment(QtCore.Qt.AlignRight|QtCore.Qt.AlignTrailing|QtCore.Qt.AlignVCenter)
            self.label.setObjectName("label")
            self.gridLayout.addWidget(self.label, 0, 2, 1, 1)
            self.label_2 = QtWidgets.QLabel(Frame)
            self.label_2.setLayoutDirection(QtCore.Qt.RightToLeft)
            self.label_2.setAlignment(QtCore.Qt.AlignRight|QtCore.Qt.AlignTrailing|QtCore.Qt.AlignVCenter)
            self.label_2.setObjectName("label_2")
            self.gridLayout.addWidget(self.label_2, 2, 2, 1, 1)
            self.btnoutput = QtWidgets.QPushButton(Frame)
            self.btnoutput.setStyleSheet("background-color: rgb(233, 185, 110);")
            self.btnoutput.setObjectName("btnoutput")
            self.gridLayout.addWidget(self.btnoutput, 2, 5, 1, 1)
    
            self.btnoutput.clicked.connect(self.BrowseOutput_Dir)
    
    
            self.lstrarfiles = QtWidgets.QListWidget(Frame)
            self.lstrarfiles.setObjectName("lstrarfiles")
            self.gridLayout.addWidget(self.lstrarfiles, 1, 4, 1, 1)
    
            self.retranslateUi(Frame)
            QtCore.QMetaObject.connectSlotsByName(Frame)
            Frame.setTabOrder(self.btninput, self.txtoutput)
            Frame.setTabOrder(self.txtoutput, self.btnoutput)
            Frame.setTabOrder(self.btnoutput, self.btnextract)
    
        def retranslateUi(self, Frame):
            _translate = QtCore.QCoreApplication.translate
            Frame.setWindowTitle(_translate("Frame", "UnRar - Master"))
            self.btninput.setText(_translate("Frame", "Browse"))
            self.btnextract.setText(_translate("Frame", "Extract"))
            self.label.setText(_translate("Frame", "Rar File :"))
            self.label_2.setText(_translate("Frame", "Unrar Dir :"))
            self.btnoutput.setText(_translate("Frame", "Browse"))
    
        def BrowseInput_Path(self):
            path = QtWidgets.QFileDialog.getOpenFileNames(filter='*.rar')
            for eachfile in path:
                self.lstrarfiles.addItems(eachfile)
        def BrowseOutput_Dir(self):
            Dir_Path = str(QtWidgets.QFileDialog.getExistingDirectory())
            self.txtoutput.setText(Dir_Path)
        def Extract(self):
            lst = self.lstrarfiles
            for eachitem in range(lst.count()-1):
                RarFile = str(lst.item(eachitem).text())
                patoolib.extract_archive(RarFile, outdir=self.txtoutput.text())
            QtWidgets.QMessageBox.about(self.Frame,"Status","Completed")
    if __name__ == "__main__":
        
        app = QtWidgets.QApplication(sys.argv)
        Frame = QtWidgets.QFrame()
        ui = Ui_Frame()
        ui.setupUi(Frame)
        Frame.show()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
