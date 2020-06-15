---
title: pyqt5_4
date: 2020-05-07
---
Example Python program pyqt5_4.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtWidgets import (QApplication, QWidget, QComboBox, QDialog,
* from PyQt5.QtGui import QIcon
* import sys
* import os
* import re

## Classes

* class MainWindow(QWidget):
* class SubWindow:

## Methods

* def __init__(self,parent=None):
* def makeWindow(self):
* def __init__(self,x,y,parent=None):
* def show(self):

## Code

Example Python PyQt program :

    #!/usr/bin/env python
    from PyQt5.QtWidgets import (QApplication, QWidget, QComboBox, QDialog,
            QDialogButtonBox, QFormLayout, QGridLayout, QGroupBox, QHBoxLayout,
            QLabel, QLineEdit, QMenu, QMenuBar, QPushButton, QSpinBox, QTextEdit,
            QVBoxLayout)
    from PyQt5.QtGui import QIcon
    
    import sys
    import os
    import re
    
    class MainWindow(QWidget):
    
        def __init__(self,parent=None):
            #super() でスーパークラスのインスタンスメソッドを呼び出す
            super(MainWindow, self).__init__(parent)
            #ボタンの作成
            self.button=QPushButton("Push")
            #ボタンをクリックした場合、makeWindowを実行
            self.button.clicked.connect(self.makeWindow)
            #ボタンレイアウト
            button_Layout= QVBoxLayout()
            #Widget追加
            button_Layout.addWidget(self.button)
            #ラベル
            self.x = 0
            self.y = 0
            self.input_label_x = QLabel("Input X");
            #x_入力フォーム
            self.input_x = QLineEdit()
    
            self.input_label_y = QLabel("Input Y");
            #y_入力フォーム
            self.input_y = QLineEdit()
    
            #とりあえずテキストとボタンのlyaoutを分ける
            text_Layout = QVBoxLayout()
            text_Layout.addWidget(self.input_label_x)
            text_Layout.addWidget(self.input_x)
            text_Layout.addWidget(self.input_label_y)
            text_Layout.addWidget(self.input_y)
    
            #レイアウト、QVBoxLayoutのインスタンス
            mainLayout = QVBoxLayout()
            #textのレイアウトを追加
            mainLayout.addLayout(text_Layout)
            #ボタンのレイアウトを追加
            mainLayout.addLayout(button_Layout)
            #QVBoxLayoutをaddWidgetを追加したものに更新
            self.setLayout(mainLayout)
            #windowのタイトル変更
            self.setWindowTitle("Test App4")
    
        def makeWindow(self):
            #xが数値か判定 正規表現
            if bool(re.compile("^\d+\.?\d*\Z").match(self.input_x.text())):
                #xを代入
                self.x = float(self.input_x.text())
                #yが数値か判定　正規表現
                if bool(re.compile("^\d+\.?\d*\Z").match(self.input_y.text())):
                    #yを代入
                    self.y = float(self.input_y.text())
                    #subWindowのインスタンス作成
                    subWindow = SubWindow(self.x,self.y)
                    #subWindowを表示
                    subWindow.show()
    
    class SubWindow:
        def __init__(self,x,y,parent=None):
    
            #QDialogのインスタンス
            self.w = QDialog(parent)
            self.x = x
            self.y = y
            self.z = self.x*self.y
            self.sub_label1 = QLabel()
            self.sub_label1.setText(str(self.x)+"×"+str(self.y)+"="+str(self.z))
    
            layout = QVBoxLayout()
            layout.addWidget(self.sub_label1)
    
            #レイアウトを設定する
            self.w.setLayout(layout)
    
        def show(self):
            self.w.exec_()
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        path = os.path.join(os.path.dirname(sys.modules[__name__].__file__), 'ico.png')
        app.setWindowIcon(QIcon(path))
        P = MainWindow()
        P.show()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
