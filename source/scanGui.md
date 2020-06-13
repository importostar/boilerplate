---
title: scanGui
date: 2020-05-07
---
Example Python program scanGui.py
This program creates a PyQt GUI

## Modules

* import sys
* import os
* import time
* from datetime import datetime
* from glob import glob
* from gui.window import Ui_MainWindow
* from scan import ScanMotors
* from PyQt5 import QtWidgets
* from PyQt5.QtCore import QThread, QObject, pyqtSlot, pyqtSignal
* from PyQt5.QtWidgets import QMessageBox
* from PyQt5.QtGui import QTextCursor
* from py4syn.utils.scan import scanDataToLine, scanHeader, setPlotGraph
* #from PyQt5 import QtWidgets
* #from PyQt5.QtWidgets import QMessageBox
* #from PyQt5.QtCore import QObject, pyqtSlot
* #import sys
* #import pyqthandler
* #from PyQtArgs.qtArgs import qtArgs
* #from datetime import timedelta
* #from threading import Lock

## Classes

* class ScanMotorsT(ScanMotors, QThread):
* class ScanGui(QObject):

## Methods

* def __init__(self, arg, writeSlot):
* def run(self):
* def preScanCallback(self, counters, rows, cols, **kwargs):
* def postPointCallback(self, countersConf, counters, configuration, constants, **kwargs):
* def __init__(self, ui):
* def toggleStartStop(self):
* def start(self):
* def stop(self):
* def callScan(self):
* def showDialog(self, title, text):
* def appendText(self, text):
* def finish(self):

## Code

Example Python PyQt program :

    #!/usr/bin/env python3.4
    """An interface for scan on pyqt """
    import sys
    import os
    import time
    from datetime import datetime
    from glob import glob
    
    from gui.window import Ui_MainWindow
    from scan import ScanMotors
    
    from PyQt5 import QtWidgets
    from PyQt5.QtCore import QThread, QObject, pyqtSlot, pyqtSignal
    from PyQt5.QtWidgets import QMessageBox
    from PyQt5.QtGui import QTextCursor
    from py4syn.utils.scan import scanDataToLine, scanHeader, setPlotGraph
    
    #from PyQt5 import QtWidgets
    #from PyQt5.QtWidgets import QMessageBox
    #from PyQt5.QtCore import QObject, pyqtSlot
    #import sys
    #import pyqthandler
    #from PyQtArgs.qtArgs import qtArgs
    #from datetime import timedelta
    #from threading import Lock
    
    SCAN_UTILS = "/home/ABTLUS/gabriel.fedel/XRF/scan-utils-XRF-tela/*.*.yml"
    
    class ScanMotorsT(ScanMotors, QThread):
        """A thread for scan motors
        This class encapsulate scan in a thread"""
        writeSignal = pyqtSignal(str)
        def __init__(self, arg, writeSlot):
            ScanMotors.__init__(self, args = arg)
            QThread.__init__(self)
            self.writeSignal.connect(writeSlot)
            setPlotGraph(False)
    
        def run(self):
            ScanMotors.runScan(self)
    
        def preScanCallback(self, counters, rows, cols, **kwargs):
            self.writeSignal.emit(scanHeader()+ "\n")
            ScanMotors.preScanCallback(self, counters, rows, cols, **kwargs)
    
        def postPointCallback(self, countersConf, counters, configuration, constants, **kwargs):
            self.writeSignal.emit(scanDataToLine(format="4") + "\n")
            ScanMotors.postPointCallback(self, countersConf, counters, configuration, constants, **kwargs)
    
    
    
    class ScanGui(QObject):
        def __init__(self, ui):
            super().__init__()
    
            self.ui = ui
            self.ui.btnStart.released.connect(self.start)
            self.ui.btnStart.released.connect(self.toggleStartStop)
            self.ui.btnStop.released.connect(self.stop)
    
            self.sc = None
    
            # list all counters
            counFiles = glob(SCAN_UTILS)
            self.ui.cmbCounter.addItems(sorted([c.split(".yml")[0].split(".")[-1] for c in counFiles]))
            self.ui.cmbCounter.currentIndex = 0
    
        @pyqtSlot()
        def toggleStartStop(self):
            self.ui.btnStop.setEnabled(not self.ui.btnStop.isEnabled())
            self.ui.btnStart.setEnabled(not self.ui.btnStart.isEnabled())
    
        @pyqtSlot()
        def start(self):
            self.nextRun = 0
            self.callScan()
    
        @pyqtSlot()
        def stop(self):
            # set nextRun 0 to cancell all next runs
            self.nextRun = 0
    
        def callScan(self):
            """Call scan script"""
    
            fmt = '%Y%m%d%H%M%S'  # timestamp format: year month day hour minute
            experiment = 'scan_points'  +\
                        datetime.fromtimestamp(time.time()).strftime(fmt)
            filePath = self.ui.lePath.text() + '/' + experiment
            if not os.path.exists(filePath):
                try:
                    os.makedirs(filePath)
    
                    self.arguments = {'motor': None, 'initial': None, 'final': None,
                            'stepOrCount': None, 'steps':  None, 'acquisitionTime': None,
                            'relative': None,'sync': None, 'output' : None, 'sleep': 0.0,
                            'message': None, 'optimum': None, 'time': None, 'count': 1}
    
                    # Colect the arguments from window
                    self.arguments['output'] = filePath + '/data' 
                    self.arguments['configuration'] = self.ui.cmbCounter.currentText()
    
                    row = self.nextRun
    
    #                try:
                    m1Init = self.ui.twRuns.item(row, 0).text()
                    m1End = self.ui.twRuns.item(row, 1).text()
                    m1Step = self.ui.twRuns.item(row, 2).text()
                    m2Init = self.ui.twRuns.item(row, 3).text()
                    m2End = self.ui.twRuns.item(row, 4).text()
                    m2Step = self.ui.twRuns.item(row, 5).text()
                    cntTime = self.ui.twRuns.item(row, 6).text()
    
                    # verify if all fields has data
                    if (m1Init != "" and m1End != "" and m1Step != "" and
                       m2Init != "" and m2End != "" and m2Step != "" and
                       cntTime != ""):
                        #TODO: fix to use 1 motor
                        self.arguments['initial'] = [float(m1Init), float(m2Init)]
                        self.arguments['final'] = [float(m1End), float(m2End)]
                        self.arguments['steps'] = [float(m1Step),float(m2Step)]
                        self.arguments['time'] = float(cntTime)/1000 # in seconds
    
                        self.arguments['motor'] = [self.ui.cmbMotor1.currentText(),self.ui.cmbMotor2.currentText()]
    
                        self.ui.tbOutput.append("===== Run %d ===== \n" %
                                                (self.nextRun + 1))
    
    
                        self.sc = ScanMotorsT(self.arguments, self.appendText)
                        self.sc.start()
                        self.sc.finished.connect(self.stop)
                        self.sc.finished.connect(self.toggleStartStop)
    
    #                except AttributeError:
                        # when some field is empty
    #                    pass
    
                    # there are more runs increase nextRow, else it receives 0
                    if self.ui.twRuns.rowCount() > row + 1:
                        self.nextRun += 1
                    else:
                        self.nextRun = 0
    
    
                except PermissionError:
                    self.showDialog("Directory Error", "Permission Error on Directory")
            else:
                self.showDialog("Directory Error", "Directory already exists")
    
        @pyqtSlot(str, str)
        def showDialog(self, title, text):
            """Show a simple message dialog"""
            msg = QMessageBox()
            msg.setIcon(QMessageBox.Information)
            msg.setText(text)
            msg.setWindowTitle(title)
            msg.exec_()
    
        @pyqtSlot(str)
        def appendText(self, text):
            self.ui.tbOutput.moveCursor(QTextCursor.End)
            self.ui.tbOutput.insertPlainText( text )
    
        @pyqtSlot()
        def finish(self):
            self.showDialog("terminou","terminou")
    
    if __name__ == "__main__":
        app = QtWidgets.QApplication(sys.argv)
        MainWindow = QtWidgets.QMainWindow()
        ui = Ui_MainWindow()
        ui.setupUi(MainWindow)
        MainWindow.show()
    
        sg = ScanGui(ui)
    
        sys.exit(app.exec_())
    #a = scanMotorsT()
    #a.start()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
