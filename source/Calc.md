---
title: Calc
date: 2020-05-07
---
Example Python program Calc.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5 import QtCore, QtGui, QtWidgets
* from p01 import Ui_p01  # @UnresolvedImport
* from PyQt5.uic.Compiler.qtproxies import QtCore
* from PyQt5.Qt import QApplication
* from signal import signal

## Classes

* class Test(QtWidgets.QWidget, Ui_p01):

## Methods

* def __init__(self, parent=None):
* def pr01(self, n1, n2):
* def clear(self, n1, n2):
* def radCheck(self, n1, n2, r):
* def calc(self, n1, n2, r):
* def main(args):

## Code

Example Python PyQt program :

    #!/usr/bin/env pythonw
    # -*- coding: utf-8 -*-
    
    import sys
    from PyQt5 import QtCore, QtGui, QtWidgets
    from p01 import Ui_p01  # @UnresolvedImport
    from PyQt5.uic.Compiler.qtproxies import QtCore
    from PyQt5.Qt import QApplication
    from signal import signal
    
    class Test(QtWidgets.QWidget, Ui_p01):
        def __init__(self, parent=None):
            super(Test, self). __init__(parent)
            self.ui = Ui_p01()
            self.setupUi(self)
            self.calcButton.clicked.connect(lambda: self.pr01(self.n1.text(), self.n2.text()))
    
        def pr01(self, n1, n2):
            if not n1 or not n2:
                self.ans.setText("Failed")
            else:
                r = 0
                if self.radix_16.isChecked():
                    if self.radCheck(n1,n2,16):
                        n1 = int(n1, 16)
                        n2 = int(n2, 16)
                        r = 16
                    else: self.clear(n1,n2)
    
                if self.radix_2.isChecked():
                    if self.radCheck(n1,n2,2):
                        n1 = int(n1, 2)
                        n2 = int(n2, 2)
                        r = 2
                    else: self.clear(n1,n2)
    
    
                if self.radix_10.isChecked():
                    if self.radCheck(n1,n2,10):
                        n1 = float(n1)
                        n2 = float(n2)
                    else: self.clear(n1,n2)
    
                if not n1 or not n2:
                    self.ans.setText("Failed")
                else:
                    self.ans.setText(self.calc(n1, n2,r))
    
        def clear(self, n1, n2):
            n1.set("")
            n2.set("")
    
    
        def radCheck(self, n1, n2, r):
            try:
                if r == 10:
                    n1 = float(n1)
                    n2 = float(n2)
                else:
                    n1 = int(n1, r)
                    n2 = int(n2, r)
                return True
            except ValueError:
                return False
    
        def calc(self, n1, n2, r):
            res = 0
            if self.plus.isChecked():
                res = n1+n2
            elif self.minus.isChecked():
                res = n1-n2
            elif self.kakeru.isChecked():
                res = n1*n2
            elif self.waru.isChecked():
                res = n1/n2
                res = int(res)
    
            if r == 2: return bin(res)
            elif r == 16: return '%x' % res
    
            if res == int(res): return str(int(res))
            else: return str(res)
    
    def main(args):
        app = QApplication(sys.argv)
        window = Test()
        window.show()
        sys.exit(app.exec_())
    
    
    if __name__ == '__main__':
        main(sys.argv)

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
