---
title: calculator (1)
date: 2020-05-07
---
Example Python program calculator (1).py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5.QtWidgets import *
* from PyQt5.QtGui import *
* from PyQt5.QtCore import *
* import math

## Classes

* class Button:
* class Calculator(QWidget):

## Methods

* def __init__(self, text, results):
* def handle_input(self, text):
* def __init__(self, *args, **kwargs):
* def create_example_grid(self):
* def create_calculator(self):

## Code

Example Python PyQt program :

    import sys
    
    from PyQt5.QtWidgets import *
    from PyQt5.QtGui import *
    from PyQt5.QtCore import *
    import math
    
    
    class Button:
    
        def __init__(self, text, results):
            self.button = QPushButton(str(text))
            self.text = text
            self.results = results
            self.button.clicked.connect(lambda: self.handle_input(self.text))
    
        def handle_input(self, text):
            value = str(self.results.text())
            if text == "AC":
                self.results.setText("")
                return
            elif text == "+/-":
                if value[0] != "-":
                    value = "-" + value
                else:
                    value = value[1:]
            elif text == "√":
                if "+" in value or "-" in value or "/" in value or "*" in value:
                    value = eval(str(value.lstrip("0")))
                value = math.sqrt(float(value))
            elif text == "DEL":
                if len(value) > 0:
                    value = value[:-1]
            elif text == "=":
                value = eval(value.lstrip("0"))
            elif text == ".":
                if "." in value:
                    pass
                else:
                    value += str(text)
            else:
                value += str(text)
            self.results.setText(str(value))
    
    
    class Calculator(QWidget):
    
        def __init__(self, *args, **kwargs):
            super().__init__(*args, **kwargs)
            self.setWindowTitle("Calculator")
            self.create_calculator()
    
        def create_example_grid(self):
            grid = QGridLayout()
    
            button1 = QPushButton("One")
            button2 = QPushButton("Two")
            button3 = QPushButton("Three")
            button4 = QPushButton("Four")
    
            # grid.addWidget( widget , rowNumber, colNumber, rowspan ,colspan)
            grid.addWidget(button1, 0, 0, 1, 1)
            grid.addWidget(button2, 0, 1, 1, 1)
            grid.addWidget(button3, 0, 2, 1, 1)
            grid.addWidget(button4, 1, 0, 1, 3)
            self.setLayout(grid)
            self.show()
    
        def create_calculator(self):
            grid = QGridLayout()
            buttons = ["AC", "√", "DEL", "/",
                       7, 8, 9, '*',
                       4, 5, 6, "-",
                       1, 2, 3, "+",
                       0, ".", "="]
            text_input = QLineEdit("0")
            grid.addWidget(text_input, 0, 0, 1, 4)
            row = 1
            col = 0
            for button in buttons:
                if col > 3:
                    row += 1
                    col = 0
                buttonObj = Button(button, text_input)
                if button == "0":
                    grid.addWidget(buttonObj.button, row, col, 1, 2)
                    col += 1
                else:
                    grid.addWidget(buttonObj.button, row, col, 1, 1)
                col += 1
            self.setLayout(grid)
            self.show()
    
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        window = Calculator()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
