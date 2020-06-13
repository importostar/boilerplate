---
title: dial (1)
date: 2020-05-07
---
Example Python program dial (1).py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtCore import Qt
* from PyQt5.QtWidgets import (QApplication, QGridLayout, QLayout, QLineEdit,
* import sys

## Classes

* class Button(QToolButton):
* class Dialer(QWidget):

## Methods

* def __init__(self, text, parent=None):
* def sizeHint(self):
* def __init__(self, parent=None):
* def digitClicked(self):
* def backspaceClicked(self):
* def clear(self):
* def call(self):
* def createButton(self, text, member):

## Code

Example Python PyQt program :

    # Creator : Naman Tiwari (namantw)
    # To run : Make sure Python 3 is installed and PyQt5 is installed
    # Test : python dial.py <phone number>
    # For example : 'python dial.py +9872621111'
    
    from PyQt5.QtCore import Qt
    from PyQt5.QtWidgets import (QApplication, QGridLayout, QLayout, QLineEdit,
            QSizePolicy, QToolButton, QWidget)
    
    class Button(QToolButton):
        def __init__(self, text, parent=None):
            super(Button, self).__init__(parent)
    
            self.setSizePolicy(QSizePolicy.Expanding, QSizePolicy.Preferred)
            self.setText(text)
    
        def sizeHint(self):
            size = super(Button, self).sizeHint()
            size.setHeight(size.height() + 20)
            size.setWidth(max(size.width(), size.height()))
            return size
    
    
    class Dialer(QWidget):
        NumDigitButtons = 10
        
        def __init__(self, parent=None):
            super(Dialer, self).__init__(parent)
    
            phone = sys.argv[1];
            try: 
                int(phone)
            except ValueError:
                phone = 'Not a number'
    
            self.display = QLineEdit(phone)
            self.display.setReadOnly(True)
            self.display.setAlignment(Qt.AlignRight)
            self.display.setMaxLength(15)
    
            font = self.display.font()
            font.setPointSize(font.pointSize() + 8)
            self.display.setFont(font)
    
            self.digitButtons = []
            
            for i in range(Dialer.NumDigitButtons):
                self.digitButtons.append(self.createButton(str(i),
                        self.digitClicked))
    
            self.backspaceButton = self.createButton("<--",
                    self.backspaceClicked)
            self.clearButton = self.createButton("Clear", self.clear)
            self.callButton = self.createButton("Call", self.call)
    
            mainLayout = QGridLayout()
            mainLayout.setSizeConstraint(QLayout.SetFixedSize)
    
            mainLayout.addWidget(self.display, 0, 1, 1, 3)
            mainLayout.addWidget(self.backspaceButton, 1, 1, 1, 1)
            mainLayout.addWidget(self.clearButton, 1, 2, 1, 2)
    
            for i in range(1, Dialer.NumDigitButtons):
                row = ((9 - i) / 3) + 2
                column = ((i - 1) % 3) + 1
                mainLayout.addWidget(self.digitButtons[i], row, column)
    
            mainLayout.addWidget(self.digitButtons[0], 5, 1)
            mainLayout.addWidget(self.callButton, 5, 2, 1, 2)
            self.setLayout(mainLayout)
    
            self.setWindowTitle("Dialer")
    
        def digitClicked(self):
            clickedButton = self.sender()
            digitValue = int(clickedButton.text())
    
            if self.display.text() == '0' and digitValue == 0.0:
                return
    
            if self.display.text() == '0':  
                self.display.setText(str(digitValue))
                return
    
            self.display.setText(self.display.text() + str(digitValue))
    
    
        def backspaceClicked(self):
            text = self.display.text()[:-1]
            if not text:
                text = '0'
    
            self.display.setText(text)
    
        def clear(self):
            self.display.setText('0')
    
        def call(self):
            #Well :( ummm.... Not ready to call yet
            return
    
        def createButton(self, text, member):
            button = Button(text)
            button.clicked.connect(member)
            return button
    
    
    if __name__ == '__main__':
    
        import sys
    
        app = QApplication(sys.argv)
        dialer = Dialer()
        dialer.show()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
