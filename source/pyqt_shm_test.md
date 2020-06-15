---
title: pyqt_shm_test
date: 2020-05-07
---
Example Python program pyqt_shm_test.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import time
* from PyQt5.QtCore import QTimer
* from PyQt5.QtWidgets import QWidget, QVBoxLayout, QProgressBar, QPushButton
* import multiprocessing
* from multiprocessing import shared_memory
* import numpy as np
* import sys
* from PyQt5.QtWidgets import QApplication

## Classes

* class DataPuller(multiprocessing.Process):
* class Window(QWidget):

## Methods

* def __init__(
* def run(self):
* def __init__(self, *args, **kwargs):
* def onStart(self):
* def onTimer(self):
* def closeEvent(self, event):

## Code

Example Python PyQt program :

    import time
    from PyQt5.QtCore import QTimer
    from PyQt5.QtWidgets import QWidget, QVBoxLayout, QProgressBar, QPushButton
    import multiprocessing
    from multiprocessing import shared_memory
    import numpy as np
    
    DATA_SIZE = 1
    DTYPE = np.int64
    
    
    class DataPuller(multiprocessing.Process):
        def __init__(
                self,
                event,
                shared_mem_name,
        ):
            super().__init__()
            self.event = event
            self.counter = 0
            self.shared_mem_name = shared_mem_name
    
        def run(self):
            self.shm = shared_memory.SharedMemory(name=self.shared_mem_name)
            self.sample = np.ndarray(
                shape=(DATA_SIZE, 1), dtype=DTYPE, buffer=self.shm.buf)
            print("child process started")
            while not self.event.is_set():
                # time.sleep(0.001)
                self.sample[:, 0] = self.counter
                # print("child: ", self.sample[0, 0])
                self.counter += 1
                if self.counter >= 1000:
                    self.counter = 0
            self.shm.close()
            print("child process finished")
    
    
    class Window(QWidget):
        def __init__(self, *args, **kwargs):
            super(Window, self).__init__(*args, **kwargs)
            layout = QVBoxLayout(self)
            self.progressBar = QProgressBar(self)
            self.timer = QTimer(self)
            self.timer.timeout.connect(self.onTimer)
            self.progressBar.setRange(0, 1000)
            layout.addWidget(self.progressBar)
            layout.addWidget(QPushButton('开启线程', self, clicked=self.onStart))
    
            self.counter = 0
            self.shared_mem_name = "data"
            self.base_array = np.zeros((DATA_SIZE, 1), dtype=DTYPE)
            self.shm = shared_memory.SharedMemory(
                create=True,
                size=self.base_array.nbytes,
                name=self.shared_mem_name)
            self.sample = np.ndarray(
                shape=self.base_array.shape,
                dtype=self.base_array.dtype,
                buffer=self.shm.buf)
            self.event = multiprocessing.Event()
            self._process = DataPuller(self.event, self.shared_mem_name)
    
        def onStart(self):
            if not self._process.is_alive():
                print("main starting process")
                self._process.start()
                self.timer.start(16)
            else:
                pass
    
        def onTimer(self):
            # print("main: ", self.sample[0, 0])
            self.progressBar.setValue(self.sample[0, 0])
    
        def closeEvent(self, event):
            if self._process.is_alive():
                self.event.set()
                self._process.join()
            self.shm.close()
            self.shm.unlink()
            self.close()
            print("main process finished")
    
    
    if __name__ == '__main__':
        # need this to match OSX on Windows
        multiprocessing.set_start_method("spawn")
        import sys
        from PyQt5.QtWidgets import QApplication
        app = QApplication(sys.argv)
        w = Window()
        w.show()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
