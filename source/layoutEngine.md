---
title: layoutEngine
date: 2020-05-07
---
Example Python program layoutEngine.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from defcon import LayoutEngine
* from PyQt5.QtCore import pyqtSignal, Qt
* from PyQt5.QtWidgets import QComboBox, QGridLayout, QGroupBox, QLineEdit, QRadioButton, QVBoxLayout, QWidget

## Classes

* class OpenTypeControls(QWidget):
* class PreviewWindow(QWidget):

## Methods

* def __init__(self, parent=None):
* def updateFromEngine(self, engine):
* def __init__(self, parent=None):
* def updateView(self, text):

## Code

Example Python PyQt program :

    from defcon import LayoutEngine
    from PyQt5.QtCore import pyqtSignal, Qt
    from PyQt5.QtWidgets import QComboBox, QGridLayout, QGroupBox, QLineEdit, QRadioButton, QVBoxLayout, QWidget
    
    class OpenTypeControls(QWidget):
        controlsChanged = pyqtSignal()
    
        def __init__(self, parent=None):
            super().__init__(parent)
    
            # writing direction
            ltrBox = QRadioButton("LTR", self)
            ltrBox.toggled.connect(self.controlsChanged)
            rtlBox = QRadioButton("RTL", self)
            directionGroupBox = QGroupBox("Writing direction", self)
            directionLayout = QVBoxLayout(self)
            directionLayout.addWidget(ltrBox)
            directionLayout.addWidget(rtlBox)
            directionGroupBox.setLayout(directionLayout)
            directionGroupBox.toggled.connect(self.controlsChanged)
            # script & language
            self.scriptBox = QComboBox(self)
            self.scriptBox.currentTextChanged.connect(self.controlsChanged)
            self.languageBox = QComboBox(self)
            self.languageBox.currentTextChanged.connect(self.controlsChanged)
            # feature list
            featGroupBox = QGroupBox("Feature list", self)
            featGroupBox.setFlat(True)
            self.groupBoxLayout = QVBoxLayout(self)
            featGroupBox.setLayout(self.groupBoxLayout)
            featGroupBox.toggled.connect(self.controlsChanged)
            
            layout = QVBoxLayout(self)
            layout.addWidget(directionGroupBox)
            layout.addWidget(self.scriptBox)
            layout.addWidget(self.languageBox)
            layout.addWidget(featGroupBox)
            self.setLayout(layout)
        
        def updateFromEngine(self, engine):
            # script & language
            currentText = self.scriptBox.currentText()
            self.scriptBox.clear()
            self.scriptBox.addItems(engine.getScriptList())
            self.scriptBox.setCurrentText(currentText)
            currentText = self.languageBox.currentText()
            self.languageBox.clear()
            self.languageBox.addItems(engine.getLanguageList())
            self.languageBox.setCurrentText(currentText)
            # destroy current checkboxes
            for checkBox in self.groupBoxLayout.children():
                checkBox.setParent(None)
            # populate features
            for feature in engine.getFeatureList():
                box = QCheckBox(feature, self.groupBoxLayout)
                box.setChecked(engine.getFeatureState(feature))
                #self.groupBoxLayout.addWidget(box)
            
            
    
    class PreviewWindow(QWidget):
        def __init__(self, parent=None):
            super().__init__(parent, Qt.Window)
            self._font = CurrentFont()
            self._layoutEngine = LayoutEngine(self._font)
    
            otControls = OpenTypeControls(self)
            inputLine = QLineEdit(self)
            inputLine.textChanged.connect(self.updateView)
            canvas = QWidget(self)
            
            layout = QGridLayout()
            layout.addWidget(inputLine, 0, 0, 1, 2)
            layout.addWidget(otControls, 1, 0)
            layout.addWidget(canvas, 1, 1)
            self.setLayout(layout)
        
        def updateView(self, text):
            rec = self._layoutEngine.process(text)
            print(rec)
    
    window = PreviewWindow()
    window.show()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
