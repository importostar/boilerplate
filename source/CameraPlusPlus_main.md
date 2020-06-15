---
title: CameraPlusPlus_main
date: 2020-05-07
---
Example Python program CameraPlusPlus_main.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from Camera import UsbCamera
* from posix_ipc import MessageQueue as Queue
* import os
* from PyQt5 import QtWidgets
* from PyQt5.QtWidgets import QApplication, QTabWidget
* from PyQt5.QtCore import pyqtSignal
* import sys

## Classes

* class MainWindow(QTabWidget):

## Methods

* def __init__(self):
* def wait_for_ipc(self):

## Code

Example Python PyQt program :

    from Camera import UsbCamera
    from posix_ipc import MessageQueue as Queue
    import os
    from PyQt5 import QtWidgets
    from PyQt5.QtWidgets import QApplication, QTabWidget
    from PyQt5.QtCore import pyqtSignal
    import sys
    
    q = Queue("/video_pause", flags=os.O_CREAT)
    
    
    class MainWindow(QTabWidget):
        exit_signal = pyqtSignal()
        pause_signal = pyqtSignal()
    
        def __init__(self):
            super(MainWindow, self).__init__()
            self.camera = UsbCamera()
            self.camera.setPara("Camera 1", 0)
            self.exit_signal.connect(self.camera.exitFlag)
            self.pause_signal.connect(self.camera.pauseFlag)
    
        def wait_for_ipc(self):
            while True:
                signal = str(q.receive()[0])
                print(signal)
                if signal == "b'pause'":
                    print("pause")
                    self.pause_signal.emit()
    
                if signal == "b'start'":
                    print("start")
                    self.camera.start()
    
                if signal == "b'exit'":
                    print("exit")
                    self.exit_signal.emit()
                    break
    
                if signal == "b'resume'":
                    print("resume")
                    self.pause_signal.emit()
    
    
    if __name__ == '__main__':
        app = QtWidgets.QApplication(sys.argv)
        window = MainWindow()
        window.wait_for_ipc()
        sys.exit(app.exec_())
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
