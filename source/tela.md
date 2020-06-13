---
title: tela
date: 2020-05-07
---
Example Python program tela.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5 import QtWidgets
* from ui_tela import Ui_MainWindow

## Classes

* class Tela(QtWidgets.QMainWindow):

## Methods

* def __init__(self):
* def connectSignals(self):
* def someAction(self):
* def main():

## Code

Example Python PyQt program :

    # 1-Pylestras 30/08/2016
    # QT + Python - github.com/zsinx6
    
    import sys
    
    from PyQt5 import QtWidgets
    
    from ui_tela import Ui_MainWindow
    
    
    class Tela(QtWidgets.QMainWindow):
    
        def __init__(self):
            super(Tela, self).__init__()
            # instancia a UI gerada pelo QtDesigner
            self.ui = Ui_MainWindow()
            # faz o setup inicial
            self.ui.setupUi(self)
            # faz a conexão dos sinais
            self.connectSignals()
    
        def connectSignals(self):
            # conecta os eventos
            self.ui.pushButton.clicked.connect(self.someAction)
    
        def someAction(self):
            # uma ação realizada quando o evento acontece
            self.ui.lineEdit.setText("Hello World")
    
    
    def main():
        # cria uma application do qt
        app = QtWidgets.QApplication(sys.argv)
        # instancia a classe Tela
        mw = Tela()
        # exibe a tela
        mw.show()
        # inicia a application do qt
        sys.exit(app.exec_())
    
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
