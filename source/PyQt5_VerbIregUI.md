---
title: PyQt5_VerbIregUI
date: 2020-05-07
---
Example Python program PyQt5_VerbIregUI.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import random
* import os
* from fbs_runtime.application_context import ApplicationContext
* from PyQt5.QtCore import pyqtSlot
* from PyQt5.QtWidgets import QApplication, QDialog, QMainWindow, QMessageBox
* from PyQt5.uic import loadUi

## Classes

* class MainW(QMainWindow):

## Methods

* def __init__(self):
* def on_push(self):
* def quiz(self):

## Code

Example Python PyQt program :

    import sys
    import random
    import os
    from fbs_runtime.application_context import ApplicationContext
    from PyQt5.QtCore import pyqtSlot
    from PyQt5.QtWidgets import QApplication, QDialog, QMainWindow, QMessageBox
    from PyQt5.uic import loadUi
    
    
    
    class MainW(QMainWindow):
        def __init__(self):
            super(MainW, self).__init__()
            loadUi('VerbIreg.ui', self)
            self.setWindowTitle('Verbes Ireguliers Quiz')
            self.pushButton.clicked.connect(self.on_push)
            self.pushButton2.hide()
            self.labelFirst.hide()
            self.labelSecond.hide()
            self.labelThird.hide()
            self.lineEdit2.hide()
            self.lineEdit3.hide()
            self.labelAns1.hide()
            self.labelAns2.hide()
            self.labelAns3.hide()
            self.pushButton2.clicked.connect(self.quiz)
    
        @pyqtSlot()
        def on_push(self):
            First = False
            global n
            n = int(self.lineEdit.text())
            self.pushButton.hide()
            self.pushButton2.show()
            self.labelFirst.show()
            self.labelSecond.show()
            self.labelThird.show()
            self.lineEdit.clear()
            self.lineEdit2.show()
            self.lineEdit3.show()
            self.lineEdit.setFocus()
            self.label.setText(l[r][3].title())
    
        @pyqtSlot()
        def quiz(self):
            global c,r,good,bad
            if self.lineEdit.text() == l[r][0]:
                self.labelAns1.setText("Great !")
                good += 1
            else:
                self.labelAns1.setText("Wrong! It is: "+ l[r][0])
                bad +=1
            if self.lineEdit2.text() == l[r][1]:
                self.labelAns2.setText("Great !")
                good += 1
            else:
                self.labelAns2.setText("Wrong! It is: "+ l[r][1])
                bad += 1
            if self.lineEdit3.text() == l[r][2]:
                self.labelAns3.setText("Great !")
                good += 1
            else:
                self.labelAns3.setText("Wrong! It is: "+ l[r][2])
                bad += 1
            self.labelAns3.show()
            self.labelAns2.show()
            self.labelAns1.show()
    
            if c != n :
                r = random.randint(0, len(l))
                self.label.setText(l[r][3].title())
                self.lineEdit.clear()
                self.lineEdit2.clear()
                self.lineEdit3.clear()
                self.lineEdit.setFocus()
                c+=1
            else:
                choise = QMessageBox.question(self, "Score!",
                                                    "Your Score is " + str(good) + "/" + str(good+bad)+"\n C'est qui fait "+str((good * 20) / (good+bad))+"/20" +"\n Encore un nouveau jeu?",
                                                    QMessageBox.No | QMessageBox.Yes)
                if choise == QMessageBox.No:
                    print("Au revoir")
                    sys.exit()
                else:
                    python = sys.executable
                    os.execl(python, python, * sys.argv)
    
    
    
    
    global l, n, r, c, First, bad, good
    bad = good = n = 0
    First = True
    with open('IV.csv', 'r') as file:
        f = file.readlines()
    l = []
    for line in f:
        l.append(line.split(";"))
    r = random.randint(0, len(l))
    c = 1
    app = QApplication(sys.argv)
    widget = MainW()
    widget.show()
    sys.exit(app.exec_())
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
