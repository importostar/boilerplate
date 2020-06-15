---
title: AudioPlayer
date: 2020-05-07
---
Example Python program AudioPlayer.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import numpy as np
* import pyaudio
* import pyqtgraph as pg 
* from PyQt5.QtWidgets import QMainWindow, QAction, QApplication, QMenu, QFileDialog, QWidget, QPushButton, QVBoxLayout, QGridLayout
* from PyQt5 import QtCore

## Classes

* class audioAnalyzer(QMainWindow):
* class specTrum(pg.PlotWidget):

## Methods

* def __init__(self):
* def initUI(self):
* def openFileNameDialog(self):
* def saveFileDialog(self):
* def spectrum(self):
* def record(self):
* def recordAction(self):
* def stopAction(self):
* def __init__(self):
* def initUI(self):
* def update(self):
* def input(self):

## Code

Example Python PyQt program :

    import sys
    import numpy as np
    import pyaudio
    import pyqtgraph as pg 
    from PyQt5.QtWidgets import QMainWindow, QAction, QApplication, QMenu, QFileDialog, QWidget, QPushButton, QVBoxLayout, QGridLayout
    from PyQt5 import QtCore
    
    class audioAnalyzer(QMainWindow):
        def __init__(self):
            super().__init__()
            self.initUI()
    
        def initUI(self):
            menubar = self.menuBar()
            fileMenu = menubar.addMenu('File')
            modeMenu = menubar.addMenu('Mode')
    
            openAct = QAction('Open', self)
            openAct.setShortcut('Ctrl+O')
            openAct.setStatusTip('Open a file')
            openAct.triggered.connect(self.openFileNameDialog)
    
            exitAct = QAction('Exit', self)
            exitAct.setShortcut('Esc')
            exitAct.triggered.connect(self.close)
         
            recordAct = QAction('Record', self)
            recordAct.setShortcut('Ctrl+R')
            recordAct.triggered.connect(self.record)
    
            rtMicAct = QAction('Realtime microphone analyzer', self)
            rtMicAct.setShortcut('Ctrl+A')
            rtMicAct.triggered.connect(self.spectrum)
            
            fileMenu.addAction(openAct)
            fileMenu.addAction(exitAct)
    
            modeMenu.addAction(recordAct)
            modeMenu.addAction(rtMicAct)
    
    
            self.setGeometry(446, 156, 1028, 768)
            self.setWindowTitle('Audio Analyzer')    
            self.show()
        
        def openFileNameDialog(self):
            options = QFileDialog.Options()
            options |= QFileDialog.DontUseNativeDialog
            fileName, _ = QFileDialog.getOpenFileName(self,"Open file", "","Audio File (*.wav)", options=options)
            if fileName:
                print(fileName)
    
        def saveFileDialog(self):
            options = QFileDialog.Options()
            options |= QFileDialog.DontUseNativeDialog
            fileName, _ = QFileDialog.getSaveFileName(self,"Save file","","Audio File (*.wav)", options=options)
            if fileName:
                print(fileName)
    
        def spectrum(self):
            # Spectrum  
            self.specTrum = specTrum()
            self.setCentralWidget(self.specTrum)
    
        def record(self):
            def recordAction(self):
                recordBtn.setText('Stop')
                recordBtn.setToolTip('Stop Recording')
                recordBtn.setShortcut('Ctrl+S')
                recordBtn.clicked.connect(stopAction)
    
            def stopAction(self):
                recordBtn.setText('Start')
                recordBtn.setToolTip('Start Recording')
                recordBtn.setShortcut('Ctrl+R')
                recordBtn.clicked.connect(recordAction)
    
            wid = QWidget(self)
            self.setCentralWidget(wid)
    
            recordBtn = QPushButton('Start')
            recordBtn.setToolTip('Start Recording')
            recordBtn.setShortcut('Ctrl+R')
            recordBtn.setFixedSize(50, 35)
            recordBtn.clicked.connect(recordAction)
    
            grid = QGridLayout()
            grid.addWidget(recordBtn)        
    
            vbox = QVBoxLayout()
            vbox.addStretch(1)
            vbox.addLayout(grid)      
    
            wid.setLayout(vbox)
    
            
    
    class specTrum(pg.PlotWidget):
        format = pyaudio.paFloat32
        channels = 1
        rate = 16000
        chunk = 512
        start = 0
        N = 512
    
        def __init__(self):
            super().__init__()
            self.initUI()
    
        def initUI(self):
            #PyAudio
            self.pa = pyaudio.PyAudio()
            self.stream = self.pa.open(
                format = self.format,
                channels = self.channels,
                rate = self.rate,
                input = True,
                output = False,
                frames_per_buffer = self.chunk)
    
            #PlotWidget
            self.plotitem = self.getPlotItem()
            self.plotitem.setMouseEnabled(x = False, y = False) 
            self.plotitem.setYRange(0, 10, padding = 0)
            self.plotitem.setXRange(0, 8000, padding = 0)
            self.plotSpectrum = self.plotitem.plot()
            
            #Label
            self.specAxis = self.plotitem.getAxis("bottom")
            self.specAxis.setLabel("Frequency (Hz)")        
    
            #Update plot
            self.timer = QtCore.QTimer()
            self.timer.timeout.connect(self.update)
            self.timer.start(10)
    
        def update(self):
            data = self.input()
            freqlist = np.fft.fftfreq(self.N, d = 1.0 / self.rate)
            x = np.fft.fft(data[self.start:self.start + self.N])
            amplitudeSpectrum = [np.sqrt(c.real ** 2 + c.imag ** 2) for c in x]
            self.plotSpectrum.setData(freqlist, amplitudeSpectrum)
    
        def input(self):
            data = self.stream.read(self.chunk)
            data = np.frombuffer(data, np.float32)
            return data
    
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        audioAnalyzer = audioAnalyzer()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
