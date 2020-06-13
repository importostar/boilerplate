---
title: qprocesstest
date: 2020-05-07
---
Example Python program qprocesstest.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtCore import QProcess
* from PyQt5.QtWidgets import QApplication, QFormLayout, QDialog, QTextEdit, QPushButton
* import base64
* import sys

## Classes

* class ProcessDialog(QDialog):

## Methods

* def __init__(self, cmd, args, parent=None):
* def onDataReady(self):
* def onClose(self):
* def onProcessFinished(self):

## Code

Example Python PyQt program :

    #!/usr/bin/env python3
    
    from PyQt5.QtCore import QProcess
    from PyQt5.QtWidgets import QApplication, QFormLayout, QDialog, QTextEdit, QPushButton
    import base64
    import sys
    
    class ProcessDialog(QDialog):
        def __init__(self, cmd, args, parent=None):
            QDialog.__init__(self)
            self.cmd = cmd
            self.args = args
            self.keepGoing = True
            layout = QFormLayout()
            layout.setContentsMargins(10, 10, 10, 10)
            self.output = QTextEdit()
            layout.addRow(self.output)
            self.setLayout(layout)
    
            self.closeButton = QPushButton("Close", self)
            layout.addRow(self.closeButton)
            self.closeButton.clicked.connect(self.onClose)
    
            self.ext_process = QProcess(self)
            self.ext_process.started.connect(self.open)
            self.ext_process.readyReadStandardOutput.connect(self.onDataReady)
            self.ext_process.finished.connect(self.onProcessFinished)
            self.ext_process.start(self.cmd, self.args)
    
        def onDataReady(self):
            cursor = self.output.textCursor()
            cursor.movePosition(cursor.End)
            cursor.insertText(str(base64.b64encode(self.ext_process.readAll())))
            self.output.ensureCursorVisible()
            
        def onClose(self):
            self.ext_process.close()
    
        def onProcessFinished(self):
            self.close()
    
    if __name__ == "__main__":
        app = QApplication(sys.argv)
        dlg = ProcessDialog("cat", ["/dev/random"])
        dlg.show()    
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
