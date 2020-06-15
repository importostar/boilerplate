---
title: TAFEditor
date: 2020-05-07
---
Example Python program TAFEditor.py
This program creates a PyQt GUI

## Modules

* import pytaf
* import sys
* from PyQt5.QtWidgets import (QWidget, QTextEdit, QApplication, QVBoxLayout)

## Classes

* class TAFEditor(QWidget):

## Methods

* def __init__(self):
* def tafChanged(self):

## Code

Example Python PyQt program :

    #!/usr/bin/python3
    # -*- coding: utf-8 -*-
    """
    Simple Editor for TAF with 'decoded' text shown
    
    requires:
    pip install pyqt5
    pip install pytaf
    
    """
    
    import pytaf
    import sys
    from PyQt5.QtWidgets import (QWidget, QTextEdit, QApplication, QVBoxLayout)
    
    taf_str = """
    TAF NZAA 032258Z 0400/0424
    22015G25KT 9999 BKN035
    BECMG 0410/0412 18005KT
    """
    
    class TAFEditor(QWidget):
    
        def __init__(self):
            super().__init__()
    
            self.taf_raw = QTextEdit()
            self.taf_verbose = QTextEdit()
    
            self.taf_raw.setText(taf_str)
            self.taf_raw.textChanged.connect(self.tafChanged)
            self.taf_verbose.setReadOnly(True)
            self.tafChanged()
    
            vbox = QVBoxLayout()
            vbox.addWidget(self.taf_raw)
            vbox.addWidget(self.taf_verbose)
            self.setLayout(vbox)
           
            self.setGeometry(300, 300, 800, 600)
            self.setWindowTitle('TAF Editor')
            self.show()
    
        def tafChanged(self):
    
            text = self.taf_raw.toPlainText()
            taf_object = pytaf.TAF(text)
            decoder = pytaf.Decoder(taf_object)
            decoded_str = decoder.decode_taf()
            self.taf_verbose.setText(decoded_str)
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        te = TAFEditor()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
