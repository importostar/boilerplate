---
title: validation
date: 2020-05-07
---
Example Python program validation.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5.QtCore import pyqtSignal, QRegularExpression
* from PyQt5.QtWidgets import (QApplication, QFrame, QLabel, QLineEdit,

## Classes

* class FormGroup(QWidget):
* class FormControl(QWidget):
* class Window(QWidget):

## Methods

* def __init__(self, orientation='vertical'):
* def addControl(self, control):
* def validateGroup(self, _):
* def __init__(self, title=''):
* def title(self):
* def title(self, title):
* def maximum(self):
* def maximum(self, value):
* def minimum(self):
* def minimum(self, value):
* def range(self, minimum, maximum):
* def validate(self, input_text):
* def onValid(self):
* def onInvalid(self, error_message):
* def isNumber(self, value):
* def __init__(self):
* def formValidation(self, is_valid):

## Code

Example Python PyQt program :

    import sys
    from PyQt5.QtCore import pyqtSignal, QRegularExpression
    from PyQt5.QtWidgets import (QApplication, QFrame, QLabel, QLineEdit,
                                 QHBoxLayout, QVBoxLayout, QWidget, QPushButton)
    
    class FormGroup(QWidget):
        groupValidation = pyqtSignal(bool)
        def __init__(self, orientation='vertical'):
            super().__init__()
    
            self.form_controls = []        
            self.main_layout = QVBoxLayout() if orientation == 'vertical' else QHBoxLayout()
            self.setLayout(self.main_layout)
            
        def addControl(self, control):
            if not isinstance(self, FormControl):
                self.form_controls.append(control)
                self.main_layout.addWidget(control)
                control.inputValidation.connect(self.validateGroup)
            else:
                raise ValueError('could not add object of type {}'.format(type(control)))
                
    
        def validateGroup(self, _):
            for control in self.form_controls:
                if not control.valid:
                    self.groupValidation.emit(False)
                    return
            
            self.groupValidation.emit(True)
    
    
    class FormControl(QWidget):
        inputValidation = pyqtSignal(bool)
        def __init__(self, title=''):
            super().__init__()
    
            control_layout = QVBoxLayout()
    
            self.form_label = QLabel()
            self.form_control = QLineEdit()
            self.validation_label = QLabel()
            self.validation_label.setStyleSheet('color: red')
            
            control_layout.addWidget(self.form_label)
            control_layout.addWidget(self.form_control)
            control_layout.addWidget(self.validation_label)
            control_layout.addStretch(1)
    
            self.setLayout(control_layout)
    
            self.title = title
            self.required = False
            self.required_error_message = '{} is required.'
    
            self.email = False
            self.email_error_message = 'The value should be an email.'
            self.email_regex = QRegularExpression("\\b[A-Z0-9._%+-]+@[A-Z0-9.-]+\\.[A-Z]{2,4}\\b",
                              QRegularExpression.CaseInsensitiveOption)
    
            self.number = False
            self.number_error_message = '{} should be a number.'
            self._minimum = None
            self.min_error_message = '{} should be higher than {}.'
            self._maximum = None
            self.max_error_message = '{} should be lower than {}.'
            
            
            self.valid = False
    
            self.form_control.textChanged.connect(self.validate)
    
        @property
        def title(self):
            return self._title
        
        @title.setter
        def title(self, title):
            self._title = title
            self.form_label.setText('{}:'.format(self._title))
        
        @property
        def maximum(self):
            return self._maximum
        
        @maximum.setter
        def maximum(self, value):
            self._maximum = value
            self.number = True
        
        @property
        def minimum(self):
            return self._minimum
        
        @minimum.setter
        def minimum(self, value):
            self._minimum = value
            self.number = True
        
        def range(self, minimum, maximum):
            self._minimum = minimum
            self._maximum = maximum
            self.number = True
    
        def validate(self, input_text):
            text = input_text.strip()
            if self.required and not text:
                self.onInvalid(self.required_error_message.format(self.title))
                return
            if self.email and not self.email_regex.match(text).hasMatch():
                self.onInvalid(self.email_error_message)
                return
            if self.number:
                value, ok = self.isNumber(text)
                if not ok:              
                    self.onInvalid(self.number_error_message.format(self.title))
                    return
                if self._maximum is not None and value > self._maximum:
                    self.onInvalid(self.max_error_message.format(self.title, self._maximum))
                    return
                if self._minimum is not None and value < self._minimum:
                    self.onInvalid(self.min_error_message.format(self.title, self._minimum))
                    return
            self.onValid()
    
        def onValid(self):
            self.form_control.setStyleSheet('')
            self.validation_label.setText('')
            self.valid = True
            self.inputValidation.emit(True)
    
        def onInvalid(self, error_message):
            self.form_control.setStyleSheet('border: 1px solid red;')
            self.validation_label.setText(error_message)
            self.valid = False
            self.inputValidation.emit(False)
        
        def isNumber(self, value):
            try:
                return float(value), True
            except ValueError:
                return None, False
    
    class Window(QWidget):
        def __init__(self):
            super().__init__()
            self.setWindowTitle('Validation Demo')
            self.setMinimumSize(400, 300)
            
            layout = QVBoxLayout()
    
            name = FormControl('Name')
            name.required = True
    
            email = FormControl('Email')
            email.required = True
            email.email = True
    
            age = FormControl('Age')
            age.required = True
            age.range(18, 80)
    
            self.button = QPushButton('Submit')
            self.button.setDisabled(True)
           
            self.group = FormGroup()
            self.group.groupValidation.connect(self.formValidation)
            self.group.addControl(name)
            self.group.addControl(email)
            self.group.addControl(age) 
    
            button_layout = QHBoxLayout()
            button_layout.addStretch(1)
            button_layout.addWidget(self.button)  
            
            layout.addWidget(self.group)
            layout.addLayout(button_layout)
            layout.addStretch(1)
            self.setLayout(layout)
        
        def formValidation(self, is_valid):
            if is_valid:
                self.button.setEnabled(True)
            else:
                self.button.setDisabled(True)
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
    
        w = Window()
        w.show() 
    
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
