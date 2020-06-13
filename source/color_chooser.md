---
title: color_chooser
date: 2020-05-07
---
Example Python program color_chooser.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys, re
* from PyQt5.QtCore import *
* from PyQt5.QtGui import *
* from PyQt5.QtWidgets import *

## Classes

* class SliderColorChooser(QWidget):

## Methods

* def __init__(self, parent=None):
* def setupWidgetProperties(self):
* def connectWidgets(self):
* def setupLayout(self):
* def updateHexColorBox(self):
* def updateSlidersAndSpinners(self, hexCode):
* def updateColorBox(self):
* def main():

## Code

Example Python PyQt program :

    
    import sys, re
    from PyQt5.QtCore import *
    from PyQt5.QtGui import *
    from PyQt5.QtWidgets import *
    
    
    class SliderColorChooser(QWidget):
        # Choose colors using a slider interface
        # TODO this currently uses standard Qt Widgets, maybe write some of our own?
        #      i.e. custom sliders that give a better color representation
        # TODO interface for alpha values?
    
        # Color modes
        EightBit = 1
        SixteenBit = 2
        TwentyFourBit = 3     # NOTE Only supported one now, no real option to change it anyways
        ThirtyTwoBit = 4
    
        # For formatting and printing
        HexCodeColorFormat = 'XXX'
        BGColorCSS = 'background-color:%s;'
    
        
        def __init__(self, parent=None):
            super(SliderColorChooser, self).__init__(parent)
    
            # the sliders, in a horizontal fashion
            self.rSlider = QSlider(Qt.Horizontal, self)
            self.gSlider = QSlider(Qt.Horizontal, self)
            self.bSlider = QSlider(Qt.Horizontal, self)
    
            # The spin boxex
            self.rSpinner = QSpinBox(self)
            self.gSpinner = QSpinBox(self)
            self.bSpinner = QSpinBox(self)
    
            # The color box and hex code
            self.colorBox = QFrame(self)
            self.colorBox.setFrameStyle(QFrame.Box)
            self.colorBox.setStyleSheet(self.BGColorCSS%'#000000')
    
            self.hexCodeBox = QLineEdit(self)
            self.hexCodeBox.setText('000000')
    
            self.badHexCode = QLabel('X')       # TODO replace with a better thing, like a caution sign
            self.badHexCode.hide()              # It should only show on a bad hex color
    
            # Setup the layout
            self.setupWidgetProperties()
            self.connectWidgets()
            self.setupLayout()
    
            print(self.rSpinner.minimumSizeHint())
            print(self.rSpinner.sizeHint())
    
            print(self.rSpinner.minimumSize())
            print(self.rSpinner.size())
            print(self.rSpinner.maximumSize())
    
    
        def setupWidgetProperties(self):
            # Organization function to set properties for the widgets
    
            # Mins & Maxes
            self.rSlider.setMinimum(0x00)
            self.gSlider.setMinimum(0x00)
            self.bSlider.setMinimum(0x00)
    
            self.rSpinner.setMinimum(0x00)
            self.gSpinner.setMinimum(0x00)
            self.bSpinner.setMinimum(0x00)
    
            self.rSlider.setMaximum(0xFF)
            self.gSlider.setMaximum(0xFF)
            self.bSlider.setMaximum(0xFF)
    
            self.rSpinner.setMaximum(0xFF)
            self.gSpinner.setMaximum(0xFF)
            self.bSpinner.setMaximum(0xFF)
    
            # Steps
            self.rSlider.setSingleStep(1)
            self.gSlider.setSingleStep(1)
            self.bSlider.setSingleStep(1)
    
            self.rSpinner.setSingleStep(1)
            self.gSpinner.setSingleStep(1)
            self.bSpinner.setSingleStep(1)
    
            self.rSlider.setPageStep(8)
            self.gSlider.setPageStep(8)
            self.bSlider.setPageStep(8)
    
    
        def connectWidgets(self):
            # Organizational function to connect up all of the widget's signals and slots
    
            # Make the sliders change the spinners
            self.rSlider.valueChanged[int].connect(self.rSpinner.setValue)
            self.gSlider.valueChanged[int].connect(self.gSpinner.setValue)
            self.bSlider.valueChanged[int].connect(self.bSpinner.setValue)
    
            # Make the spinners change the sliders
            self.rSpinner.valueChanged[int].connect(self.rSlider.setValue)
            self.gSpinner.valueChanged[int].connect(self.gSlider.setValue)
            self.bSpinner.valueChanged[int].connect(self.bSlider.setValue)
    
            # Make the sliders & spinners change the contents in the box
            self.rSlider.valueChanged.connect(self.updateHexColorBox)
            self.gSlider.valueChanged.connect(self.updateHexColorBox)
            self.bSlider.valueChanged.connect(self.updateHexColorBox)
            self.rSpinner.valueChanged.connect(self.updateHexColorBox)
            self.gSpinner.valueChanged.connect(self.updateHexColorBox)
            self.bSpinner.valueChanged.connect(self.updateHexColorBox)
    
            # Make the box change the spinners and the box
            self.hexCodeBox.textEdited[str].connect(self.updateSlidersAndSpinners)
    
            # Make all of the widgets update the color in the box
            self.rSlider.valueChanged.connect(self.updateColorBox)
            self.gSlider.valueChanged.connect(self.updateColorBox)
            self.bSlider.valueChanged.connect(self.updateColorBox)
            self.rSpinner.valueChanged.connect(self.updateColorBox)
            self.gSpinner.valueChanged.connect(self.updateColorBox)
            self.bSpinner.valueChanged.connect(self.updateColorBox)
            self.hexCodeBox.textEdited.connect(self.updateColorBox)
    
    
        def setupLayout(self):
            # Organizational function to setup the layout of the widget
            layout = QGridLayout(self)
    
            # Labels
            layout.addWidget(QLabel('R', self), 0, 0)
            layout.addWidget(QLabel('G', self), 1, 0)
            layout.addWidget(QLabel('B', self), 2, 0)
    
            # Sliders
            layout.addWidget(self.rSlider, 0, 1)
            layout.addWidget(self.gSlider, 1, 1)
            layout.addWidget(self.bSlider, 2, 1)
    
            # Spinners
            layout.addWidget(self.rSpinner, 0, 2)
            layout.addWidget(self.gSpinner, 1, 2)
            layout.addWidget(self.bSpinner, 2, 2)
    
            # colors representations
            layout.addWidget(self.colorBox, 0, 3, 2, 2)
            layout.addWidget(self.hexCodeBox, 2, 3)
            layout.addWidget(self.badHexCode, 2, 4)
    
            self.setLayout(layout)
    
            # TODO set fixed width on all widgets
    
    
        @pyqtSlot()
        def updateHexColorBox(self):
            # When a slider or spinner changes, this will update the hex value in the box
            # Doesn't really matter where we get the colors from, they shoould all be the same
            rVal = self.rSlider.value()
            gVal = self.gSlider.value()
            bVal = self.bSlider.value()
    
            # Change text and hide error
            self.hexCodeBox.setText(self.HexCodeColorFormat%(rVal, gVal, bVal))
            self.badHexCode.hide()
    
    
        @pyqtSlot(str)
        def updateSlidersAndSpinners(self, hexCode):
            # Change the values of the slider and the spinners based upon the hex code
            hexCode = hexCode.strip().upper()       # Use upper case and strip
    
            # Do nothing if we don't have anything
            if len(hexCode) == 0:
                return
    
            # For our pound signers
            if hexCode[0] == '#':
                hexCode = hexCode[1:]
    
            # Make sure that we only have six chars
            if len(hexCode) != 6:
                self.badHexCode.show()
                return
    
            # Make sure that it's only hex
            x = re.compile('[0-9A-F]+')
            if x.fullmatch(hexCode) == None:
                self.badHexCode.show()
                return
    
            # Peel out each color
            rVal = int(hexCode[:2], 16)
            gVal = int(hexCode[2:4], 16)
            bVal = int(hexCode[4:], 16)
    
            # Set the spinners and the sliders
            self.rSlider.setValue(rVal)
            self.gSlider.setValue(gVal)
            self.bSlider.setValue(bVal)
            self.rSpinner.setValue(rVal)
            self.gSpinner.setValue(gVal)
            self.bSpinner.setValue(bVal)
    
    
        @pyqtSlot()
        def updateColorBox(self):
            # Get colors from sliders, not that it matters
            rVal = self.rSlider.value()
            gVal = self.gSlider.value()
            bVal = self.bSlider.value()
    
            # Build the hex code color and set the stylesheet
            hexCodeColor = '#' + self.HexCodeColorFormat%(rVal, gVal, bVal)
            self.colorBox.setStyleSheet(self.BGColorCSS%hexCodeColor)
    
    
    
    
    def main():
        app = QApplication(sys.argv)
        scc = SliderColorChooser()
        scc.show()
    
        sys.exit(app.exec_())
    
    
    main()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
