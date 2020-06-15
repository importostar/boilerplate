---
title: KPDR900_GUI
date: 2020-05-07
---
Example Python program KPDR900_GUI.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5.QtCore import (Qt, QTime)
* from PyQt5.QtWidgets import (QGridLayout, QHBoxLayout, QLabel, QLineEdit,
* import os
* import datetime
* import io
* import functools
* import serial
* import KPDR900_serial
* import logging
* import sys
* from PyQt5.QtWidgets import QApplication

## Classes

* class defaults:
* class GUI(QWidget):

## Methods

* def __init__(self, parent=None):
* def make_datalogger_box(self):
* def make_serial_box(self):
* def make_term_box(self):
* def make_info_box(self):
* def write_serial(self,msg):
* def updatetermLog(self):
* def termSubmit(self):
* def query(self,item):
* def queryinfo(self):
* def queryall(self):
* def notimplemented(self):
* def toggleLogging(self):
* def changeLog(self):
* def setTimer(self):
* def setSource(self):
* def start(self):
* def stop(self):
* def download(self):

## Code

Example Python PyQt program :

    from PyQt5.QtCore import (Qt, QTime)
    from PyQt5.QtWidgets import (QGridLayout, QHBoxLayout, QLabel, QLineEdit,
            QMessageBox, QPushButton, QTextEdit, QVBoxLayout, QWidget, QGroupBox,
            QTimeEdit, QComboBox, QSpinBox, QCheckBox, QApplication)
    
    import os
    import datetime
    import io
    import functools
    import serial
    import KPDR900_serial
    import logging
    
    class defaults:
        PCtimeout = 5
        PCport = "COM1"
        PCbaud = 19200
        logfilename = "KPDR900_log.txt"
        downloadfilename = os.path.join("data",datetime.datetime.now().strftime("%Y%m%d%H%M") + ".csv")
    
    class GUI(QWidget):
        def __init__(self, parent=None):
            super(GUI, self).__init__(parent)
    
            self.ADC = QLabel('?')
            self.BRC = QLabel('?')
            self.FVC = QLabel('?')
            self.HVC = QLabel('?')
            self.SNC = QLabel('?')
            self.TIC = QLabel("?")
            self.DLT = QLabel("?")
            self.DLS = QLabel("?")
            self.DLC = QLabel("?")
            self.ALH = QLabel("?")
            self.ALL = QLabel("?")
            self.ACH = QLabel("?")
            self.ACL = QLabel("?")
            self.PCport = QLabel(defaults.PCport)
            self.PCbaud = QLabel(str(defaults.PCbaud))
            self.PCtimeout =QLabel(str(defaults.PCtimeout))
            self.serial = serial.Serial(port=self.PCport.text(),baudrate=int(self.PCbaud.text()),timeout=int(self.PCtimeout.text()))
            self.pdr = KPDR900_serial.KPDR900(self.serial,logfile=defaults.logfilename)
            
            datalogger_box = self.make_datalogger_box()
            serial_box = self.make_serial_box()
            term_box = self.make_term_box()
            info_box = self.make_info_box()
    
            self.termLog_text = io.StringIO()
            self.logger = logging.getLogger()
            assert len(self.logger.handlers) == 1
            self.logfileHandler = self.logger.handlers[0]
            self.logconsoleHandler = logging.StreamHandler(self.termLog_text)
            self.logger.addHandler(self.logconsoleHandler)
    
            mainLayout = QGridLayout()
            mainLayout.addWidget(serial_box,0,0)
            mainLayout.addWidget(datalogger_box,0,1)
            mainLayout.addWidget(info_box,1,0)
            mainLayout.addWidget(term_box,1,1)
    
            self.setLayout(mainLayout)
            self.setWindowTitle("KPDR900")
    
        def make_datalogger_box(self):
            box = QGroupBox("DataLogger & Terminal Log")
            g = QGridLayout()
    
            labelnames = ["Current","Timer (DLT)", "Source (DLS)", "Control (DLC)", 
                          "Download Filename", "Log Filename"]
            labelpos = [(0,1), (1,0), (2,0), (3,0), (4,0), (5,0)]
    
            for i in range(len(labelnames)):
                g.addWidget(QLabel(labelnames[i]),*labelpos[i])
            
            values = {self.DLT : (1,1), self.DLS : (2,1), self.DLC : (3,1)}
            for v,p in values.items():
                g.addWidget(v,*p)
    
            #self.timerEdit = QLineEdit()
            #self.timerEdit.setInputMask("99:59:59")
            self.timerEdit = QTimeEdit()
            self.timerEdit.setMaximumTime(QTime(99,59,59)) # Maximum maximum is 24h =(
            self.timerEdit.setMinimumTime(QTime(0,0,0))
            self.timerEdit.setTime(QTime(0,0,30))
            self.timerEdit.setDisplayFormat("HH:mm:ss")
            self.sourceMenu = QComboBox()
            self.sourceMenu.addItems(["PR1","PR2","PR3"])
    
            self.downloadfileLine = QLineEdit()
            self.downloadfileLine.setText(defaults.downloadfilename)
            self.logfileLine = QLineEdit()
            self.logfileLine.setText(defaults.logfilename)
            g.addWidget(self.timerEdit,1,2)
            g.addWidget(self.sourceMenu,2,2)
            g.addWidget(self.downloadfileLine,4,1,1,2)
            g.addWidget(self.logfileLine,5,1,1,2)
    
            self.startButton = QPushButton("Start")
            self.stopButton = QPushButton("Stop")
            g.addWidget(self.startButton,3,2)
            g.addWidget(self.stopButton,3,3)
    
            self.timerButton = QPushButton("Set")
            self.sourceButton = QPushButton("Set")
            self.downloadButton = QPushButton("Download")
            self.loggingCheck = QCheckBox("Logging Enabled")
            self.loggingCheck.setChecked(True)
            g.addWidget(self.timerButton,1,3)
            g.addWidget(self.sourceButton,2,3)
            g.addWidget(self.downloadButton,4,3)
            g.addWidget(self.loggingCheck,5,3)
    
            # TODO: add callback functions to the various buttons.
            self.loggingCheck.stateChanged.connect(self.toggleLogging)
            self.logfileLine.editingFinished.connect(self.changeLog)
    
            self.timerButton.clicked.connect(self.setTimer)
            self.sourceButton.clicked.connect(self.setSource)
    
            self.startButton.clicked.connect(self.start)
            self.stopButton.clicked.connect(self.stop)
            self.downloadButton.clicked.connect(self.download)
    
            box.setLayout(g)
            return box
    
        def make_serial_box(self):
            box = QGroupBox("Serial")
            g = QGridLayout()
    
            labels = {"PC Port" : (1,0), "PC Rate" : (2,0), "PC Timeout (s)" : (3,0),
                      "KPDR900 Address" : (5,0), "KPDR900 Rate" : (6,0),
                      "Current" : (0,1)}
    
            for l,p in labels.items():
                g.addWidget(QLabel(l),*p)
    
            values = {self.PCport : (1,1), self.PCbaud : (2,1), self.PCtimeout : (3,1),
                      self.ADC : (5,1), self.BRC : (6,1)}
            for v,p in values.items():
                g.addWidget(v,*p)
    
            
            self.portLine = QLineEdit()
            self.portLine.setText(defaults.PCport)
            self.PCrateMenu = QComboBox()
            baud_rates = list(map(str,[2400,4800,9600,19200,115000]))
            self.PCrateMenu.addItems(baud_rates)
            self.PCrateMenu.setCurrentText(str(defaults.PCbaud))
            self.PCtimeoutLine = QLineEdit()
            self.PCtimeoutLine.setText(str(defaults.PCtimeout))
    
            self.PDRrateMenu = QComboBox()
            self.PDRrateMenu.addItems(baud_rates)
            self.PDRrateMenu.setCurrentText(str(defaults.PCbaud))
            self.PDRaddrMenu = QSpinBox()
            self.PDRaddrMenu.setMinimum(0)
            self.PDRaddrMenu.setMaximum(253)
            self.PDRaddrMenu.setWrapping(True)
    
            g.addWidget(self.portLine,1,2)
            g.addWidget(self.PCrateMenu,2,2)
            g.addWidget(self.PCtimeoutLine,3,2)
            g.addWidget(self.PDRaddrMenu,5,2)
            g.addWidget(self.PDRrateMenu,6,2)
    
            self.PCportButton = QPushButton("Set")
            self.PCrateButton = QPushButton("Set")
            self.PCtimeoutButton = QPushButton("Set")
            self.PDRrateButton = QPushButton("Set")
            self.PDRaddrButton = QPushButton("Set")
            self.reconnectButton = QPushButton("Reconnect")
            self.flushButton = QPushButton("Flush")
    
            g.addWidget(self.PCportButton,1,3)
            g.addWidget(self.PCrateButton,2,3)
            g.addWidget(self.PCtimeoutButton,3,3)
            g.addWidget(self.PDRrateButton,5,3)
            g.addWidget(self.PDRaddrButton,6,3)
            g.addWidget(self.reconnectButton,4,2)
            g.addWidget(self.flushButton,4,3)
    
            self.PCportButton.clicked.connect(self.notimplemented)
            self.PCrateButton.clicked.connect(self.notimplemented)
            self.PCtimeoutButton.clicked.connect(self.notimplemented)
            self.PDRrateButton.clicked.connect(self.notimplemented)
            self.PDRaddrButton.clicked.connect(self.notimplemented)
            self.reconnectButton.clicked.connect(self.notimplemented)
            self.flushButton.clicked.connect(self.notimplemented)
    
            # TODO: add callback functions to the various buttons.
    
            box.setLayout(g)
            return box        
    
        def make_term_box(self):
            box = QGroupBox("Terminal")
            v = QVBoxLayout()
            h = QHBoxLayout()
    
            self.termLog = QTextEdit()
            self.termLog.setReadOnly(True)
            self.commandLine = QLineEdit() # returnPressed() signal emitted on enterkey.
    
            self.termButton = QPushButton("Enter")
            self.clearButton = QPushButton("Clear")
            h.addWidget(self.commandLine,Qt.AlignLeft)
            h.addWidget(self.termButton)
            h.addWidget(self.clearButton)
            h.addStretch()
    
            v.addWidget(self.termLog,Qt.AlignTop)
            v.addLayout(h)
            v.addStretch()
            # TODO: add callback functions to the various buttons.
    
            self.termButton.clicked.connect(self.termSubmit)
            self.commandLine.returnPressed.connect(self.termSubmit)
            self.clearButton.clicked.connect(self.termLog.clear)
    
            box.setLayout(v)
            return box       
    
        def make_info_box(self):
            box = QGroupBox("Info")
            g = QGridLayout()
            h = QHBoxLayout()
    
            labels = {"Firmware Version" : (0,0), "Hardware Version" : (1,0), 
                      "Serial Number" : (2,0), "Time On" : (3,0)}
    
            for l,p in labels.items():
                g.addWidget(QLabel(l),*p)
    
            values = {self.FVC : (0,1), self.HVC : (1,1), self.SNC : (2,1), self.TIC : (3,1)}
            for v,p in values.items():
                g.addWidget(v,*p)
    
            
            self.queryinfoButton = QPushButton("Query Info")
            self.queryallButton = QPushButton("Query All")
            self.helpButton = QPushButton("Help")
            h.addWidget(self.queryinfoButton)
            h.addWidget(self.queryallButton)
            h.addWidget(self.helpButton)
    
            g.addLayout(h,4,0,1,2)
    
            # TODO: add callback functions to the various buttons.
            self.queryinfoButton.clicked.connect(self.queryinfo)
            self.queryallButton.clicked.connect(self.queryall)
            self.helpButton.clicked.connect(self.notimplemented)
    
            box.setLayout(g)
            return box       
    
        def write_serial(self,msg):
            #msg = self.commandLine.text()
            self.pdr.write(bytes(msg,"ASCII"))
            self.updatetermLog()
    
            # I've been told this next line is an awful hack.
            # It tells Qt to run the event loop, so the write shows up
            # on the event log, you can move the mouse a bit...
            # we kind of have to wait for the KPDR900 to answer anwyays,
            # so it's not a problem.
            QApplication.instance().processEvents()
    
            resp = self.pdr.read()
            self.updatetermLog()
    
            return resp
    
        def updatetermLog(self):
            # Snap scroll to bottom, but only if already at bottom.
            snap = False
            vsb = self.termLog.verticalScrollBar()
            if vsb.value() == vsb.maximum():
                snap = True
            self.termLog.setText(self.termLog_text.getvalue())
            if snap:
                vsb.setValue(vsb.maximum())
    
        def termSubmit(self):
            msg = self.commandLine.text()
            self.write_serial(msg)
    
        def query(self,item):
            val = str(self.write_serial("%s?" % item),'ASCII')
            getattr(self,item).setText(val.split("ACK")[1][:-3])
    
        def queryinfo(self):
            for item in ["FVC","HVC","SNC","TIC"]:
                self.query(item)
    
        def queryall(self):
            self.queryinfo()
            for item in ["ADC","BRC","DLT","DLS","DLC"]:#,"ALH","ALL","ACH","ACL"]: # Alarm+action not implemented
                self.query(item)
    
        def notimplemented(self):
            logging.warning("Not implemented.  Ask JF at jcaron@uh.edu.")
            self.updatetermLog()
    
        def toggleLogging(self):
            if self.loggingCheck.isChecked():
                self.logger.addHandler(self.logfileHandler)
            else:
                self.logger.removeHandler(self.logfileHandler)
    
        def changeLog(self):
            newfile = self.logfileLine.text()
            logging.info("Changing log file to %s" % newfile)
            self.updatetermLog()
            newhandler = logging.FileHandler(newfile)
            self.logger.addHandler(newhandler)
            self.logger.removeHandler(self.logfileHandler)
            self.logfileHandler = newhandler
            logging.info("Changed log file to %s" % newfile)
            self.updatetermLog()
    
        def setTimer(self):
            newtime = self.timerEdit.time()
            value = newtime.toString("HH:mm:ss")
            resp = self.write_serial("DLT!%s" % value)
            if b'ACK' in resp:
                self.DLT.setText(value)
    
        def setSource(self):
            #newsource = self.sourceMenu.currentData()
            #print(newsource)
            #value = newsource.toString()
            value = self.sourceMenu.currentText()
            resp = self.write_serial("DLS!%s" % value)
            if b'ACK' in resp:
                self.DLS.setText(value)
    
        def start(self):
            resp = self.write_serial("DLC!START")
            if b'ACK' in resp:
                self.DLC.setText("START")
    
        def stop(self):
            resp = self.write_serial("DLC!STOP")
            if b'ACK' in resp:
                self.DLC.setText("STOP")
    
        def download(self):
            fname = self.downloadfileLine.text()
            resp = self.write_serial("DL?")
            datalines = resp.split(b'\r')
            with open(fname,"w") as of:
                if b'Torr' not in datalines[0]:
                    logging.warning("Units not set to Torr, check log file and PDR device.")
                of.write("#time (HH:MM:SS), time (s), pressure (Torr)\n")
        
                for dline in datalines[1:-1]:
                    time_s, press_s = str(dline,'ASCII').split(";")
                    h,m,s = map(int,time_s.split(':'))
                    seconds_s = str(s + 60*(m + 60*h))
                    theline = ",".join([time_s,seconds_s,press_s])
                    of.write(theline+'\n')
            
            if not datalines[-1].endswith(b';FF'):
                logging.warning("Last line did not end with ;FF, check log file.")
    
    
    
    if __name__ == '__main__':
        import sys
    
        from PyQt5.QtWidgets import QApplication
    
        app = QApplication(sys.argv)
    
        gui = GUI()
        gui.show()
    
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
