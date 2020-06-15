---
title: haibo_cal2_gui_haibo_cal2 (1)
date: 2020-05-07
---
Example Python program haibo_cal2_gui_haibo_cal2 (1).py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os
* from PyQt5 import QtCore, QtWidgets
* from service.serviceOne import executeCal1
* from service.serviceTwo import executeCal2
* from PyQt5.QtWidgets import QApplication, QMainWindow, QFileDialog
* import sys

## Classes

* class Ui_MainWindow(QtWidgets.QWidget):

## Methods

* def setupUi(self, MainWindow):
* def OpenInputFileChooseDialog(self):
* def OpenOutputCatalogChooseDialog(self):
* def ExeCal(self):
* def retranslateUi(self, MainWindow):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'haibo_cal2.ui'
    #
    # Created by: PyQt5 UI code generator 5.8.2
    #
    # WARNING! All changes made in this file will be lost!
    import os
    
    from PyQt5 import QtCore, QtWidgets
    
    from service.serviceOne import executeCal1
    from service.serviceTwo import executeCal2
    
    
    class Ui_MainWindow(QtWidgets.QWidget):
        def setupUi(self, MainWindow):
            MainWindow.setObjectName("MainWindow")
            MainWindow.resize(397, 331)
            self.centralwidget = QtWidgets.QWidget(MainWindow)
            self.centralwidget.setObjectName("centralwidget")
            self.radioTxtType = QtWidgets.QRadioButton(self.centralwidget)
            self.radioTxtType.setGeometry(QtCore.QRect(40, 60, 89, 16))
            self.radioTxtType.setObjectName("radioTxtType")
            self.radioTxtType_2 = QtWidgets.QRadioButton(self.centralwidget)
            self.radioTxtType_2.setGeometry(QtCore.QRect(40, 90, 131, 16))
            self.radioTxtType_2.setObjectName("radioTxtType_2")
            self.text_file_input = QtWidgets.QLineEdit(self.centralwidget)
            self.text_file_input.setGeometry(QtCore.QRect(40, 140, 201, 20))
            self.text_file_input.setObjectName("text_file_input")
            self.text_file_output = QtWidgets.QLineEdit(self.centralwidget)
            self.text_file_output.setGeometry(QtCore.QRect(40, 180, 201, 20))
            self.text_file_output.setObjectName("text_file_output")
            self.button_input_choose = QtWidgets.QPushButton(self.centralwidget)
            self.button_input_choose.setGeometry(QtCore.QRect(260, 140, 111, 23))
            self.button_input_choose.setObjectName("button_input_choose")
            self.button_output_choose = QtWidgets.QPushButton(self.centralwidget)
            self.button_output_choose.setGeometry(QtCore.QRect(260, 180, 111, 23))
            self.button_output_choose.setObjectName("button_output_choose")
            self.label_execute_info = QtWidgets.QLabel(self.centralwidget)
            self.label_execute_info.setGeometry(QtCore.QRect(120, 220, 151, 16))
            self.label_execute_info.setText("")
            self.label_execute_info.setAlignment(QtCore.Qt.AlignCenter)
            self.label_execute_info.setObjectName("label_execute_info")
            self.button_execute = QtWidgets.QPushButton(self.centralwidget)
            self.button_execute.setGeometry(QtCore.QRect(160, 250, 75, 23))
            self.button_execute.setObjectName("button_execute")
            MainWindow.setCentralWidget(self.centralwidget)
            self.menubar = QtWidgets.QMenuBar(MainWindow)
            self.menubar.setGeometry(QtCore.QRect(0, 0, 397, 23))
            self.menubar.setObjectName("menubar")
            MainWindow.setMenuBar(self.menubar)
            self.statusbar = QtWidgets.QStatusBar(MainWindow)
            self.statusbar.setObjectName("statusbar")
            MainWindow.setStatusBar(self.statusbar)
    
            self.retranslateUi(MainWindow)
            QtCore.QMetaObject.connectSlotsByName(MainWindow)
    
            # =======================================================================
    
            self.button_input_choose.clicked.connect(self.OpenInputFileChooseDialog)
            self.button_output_choose.clicked.connect(self.OpenOutputCatalogChooseDialog)
            self.button_execute.clicked.connect(self.ExeCal)
    
        def OpenInputFileChooseDialog(self):
            self.inputFileName, filetype = QFileDialog.getOpenFileName(self,
                                                                       "选取文件",
                                                                       "C:/",
                                                                       "All Files (*);;Text Files (*.txt)")  # 设置文件扩展名过滤,注意用双分号间隔
            print(self.inputFileName, filetype)
            self.text_file_input.setText(self.inputFileName)
            self.targetCatalogName = os.path.dirname(self.inputFileName)
            self.text_file_output.setText(self.targetCatalogName)
    
        def OpenOutputCatalogChooseDialog(self):
            self.targetCatalogName = QFileDialog.getExistingDirectory(self, directory=self.targetCatalogName);
            self.text_file_output.setText(self.targetCatalogName)
    
        def ExeCal(self):
            self.inputFileName = self.text_file_input.text()
            self.targetCatalogName = self.text_file_output.text()
            try:
                if self.targetCatalogName == "":
                    self.label_execute_info.setText("<font color=%s>%s</font>" % ("red", "请选择输出目录"))
                elif self.radioTxtType.isChecked():
                    executeCal1(self, self.inputFileName, self.targetCatalogName)
                    self.label_execute_info.setText("<font color=%s>%s</font>" % ("green", "输出成功"))
                elif self.radioTxtType_2.isChecked():
                    executeCal2(self, self.inputFileName, self.targetCatalogName)
                    self.label_execute_info.setText("<font color=%s>%s</font>" % ("green", "输出成功"))
                elif not self.radioTxtType.isChecked() and not self.radioTxtType_2.isChecked():
                    self.label_execute_info.setText("<font color=%s>%s</font>" % ("red", "请选择一个单选内容"))
            except:
                self.label_execute_info.setText("<font color=%s>%s</font>" % ("red", "输出失败"))
    
        def retranslateUi(self, MainWindow):
            _translate = QtCore.QCoreApplication.translate
            MainWindow.setWindowTitle(_translate("MainWindow", "海波"))
            self.radioTxtType.setText(_translate("MainWindow", "test"))
            self.radioTxtType_2.setText(_translate("MainWindow", "test_shuziyuanbao"))
            self.button_input_choose.setText(_translate("MainWindow", "选择输入文件"))
            self.button_output_choose.setText(_translate("MainWindow", "选择输出文件目录"))
            self.button_execute.setText(_translate("MainWindow", "执行"))
    
    
    if __name__ == '__main__':
        from PyQt5.QtWidgets import QApplication, QMainWindow, QFileDialog
        import sys
    
        app = QApplication(sys.argv)
        MainWindow = QMainWindow()
        ui = Ui_MainWindow()
        ui.setupUi(MainWindow)
        MainWindow.show()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
