---
title: runner (1)
date: 2020-05-07
---
Example Python program runner (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from threading import Thread
* from queue import Queue, Empty
* from subprocess import *
* from enum import Enum
* from collections import defaultdict
* from PyQt5.QtWidgets import QApplication, QMainWindow
* from PyQt5.QtCore import QThread
* import traceback
* import sys
* from PyQt5.QtWidgets import QLabel, QGridLayout, QWidget, QPushButton, QLineEdit, QSpinBox
* import traceback

## Classes

* class EventEnum(Enum):
* class RunnerThread(QThread):
* class App(QApplication):
* class Gui(QWidget):

## Methods

* def fmtcmd(algo="allium", pool="stratum+tcp://garlicbois.com:3332",
* def __init__(self, parent, cmd):
* def run(self):
* def __init__(self):
* def __init__(self, app, **kwargs):
* def startminer(self):
* def cancelminer(self):

## Code

Example Python PyQt program :

    from threading import Thread
    from queue import Queue, Empty
    from subprocess import *
    from enum import Enum
    from collections import defaultdict
    
    ESCAPE = "\u001b"
    
    class EventEnum(Enum):
        cpu = "CPU"
        accepted = "[01;37m"
        block = "[36m"
        gpu = "GPU"
    
    def fmtcmd(algo="allium", pool="stratum+tcp://garlicbois.com:3332",
               maxtemp=85, intensity=None, lookupgap=None, *, user):
        sc = "ccminer-x64 --algo={} -o {} -u {} --max-temp {} {}{} {}{}"
        return sc.format(algo, pool, user, maxtemp, "--lookup-gap=" if lookupgap else "",
                         lookupgap, "--intensity=" if lookupgap else "", intensity)
        
    
    fmt = fmtcmd(intensity=13, lookupgap=2, user="GZJFrorvyt2oZLNVJUwvCY647wB5hisJFL")
    
    from PyQt5.QtWidgets import QApplication, QMainWindow
    from PyQt5.QtCore import QThread
    
    class RunnerThread(QThread):
        def __init__(self, parent, cmd):
            super().__init__()
            self.parent = parent
            self.cancelled = False
            self.cmd = cmd
            self.popen = Popen(self.cmd, stdout=PIPE, startupinfo=si)
            
        def run(self):
            try:
                while not self.cancelled or self.popen.poll() is not None:
                    msg = self.popen.stdout.readline().decode()
                    print(msg, end="")
    
                    split = msg.replace(ESCAPE, " ").split(" ")
                    try:
                        cmd = split[2]
                        val = EventEnum(cmd)
                    except Exception as e:
                        continue
                    
                    if val == EventEnum.cpu:
                        core = int(split[3][1])
                        self.cpurates[core].append(float(split[4]))
    
                    if val == EventEnum.gpu:
                        if split[4] != "Intensity":
                            try:
                                self.parent.hashrates.append(float(split[-2].strip(",")))
                                self.parent.hashrate.setText("{}KH/s".format(split[-2]))
                                self.parent.avghashrate.setText("{0:.2f}%".format(sum(self.parent.hashrates) / len(self.parent.hashrates)))
                            except:
                                pass
    
                    if val == EventEnum.block:
                        self.parent.blockno.setText("Block: {}".format(split[5]).strip(","))
    
                    if val == EventEnum.accepted:
                        success, total = split[4].split("/")
                        self.parent.percentages.append((int(success), int(total)))
                        diff = float(split[6].strip("),"))
    
                        self.parent.diffs[total] = diff
                        self.parent.hashrates.append(float(split[7]))
    
                        self.parent.success.setText("Success Percentage: {0:.2f}%".format(int(success)/int(total) * 100))
                        self.parent.difficulty.setText("Difficulty: {}".format(diff))
                        self.parent.hashrate.setText("Current Hashrate: {}kH/s".format(split[7]))
    
                        self.parent.avghashrate.setText("Avg Hashrate: {0:.2f}".format(sum(self.parent.hashrates) / len(self.parent.hashrates)))
                        self.parent.avgdifficulty.setText("Avg Difficulty: {0:.2f}".format(sum(self.parent.diffs.values()) / len(self.parent.diffs)))
                        
            except:
                import traceback
                traceback.print_exc()
            finally:
                if self.popen.poll() is None:
                    self.popen.terminate()
                else:
                    self.parent.cancelminer()
                
    
    import sys
    
    if sys.platform == "win32":
        si = STARTUPINFO()
        si.dwFlags |= SW_HIDE | STARTF_USESHOWWINDOW
    
    
    from PyQt5.QtWidgets import QLabel, QGridLayout, QWidget, QPushButton, QLineEdit, QSpinBox
    
    
    class App(QApplication):
        def __init__(self):
            super().__init__(sys.argv)
            self.gui = Gui(self)
            self.gui.show()
    
    class Gui(QWidget):
        popen = None
        thread = None
        cmd = None
        def __init__(self, app, **kwargs):
            super(__class__, self).__init__(**kwargs)
            self.app = app
            self.hashrates = []
            self.cpurates = defaultdict(list)
            self.diffs = {}
            self.percentages = []
    
            self.grid = QGridLayout(self)
            self.grid.setSpacing(8)
            self.grid.setColumnStretch(3, 1)
            
            self.success = QLabel("Success Percentage: 0%")
            self.grid.addWidget(self.success, 1, 0)
            
            self.difficulty = QLabel("Difficulty: 0")
            self.grid.addWidget(self.difficulty, 1, 1)
            
            self.hashrate = QLabel("Hashrate: 0KH/s")
            self.grid.addWidget(self.hashrate, 1, 2)
            
            self.avgdifficulty = QLabel("Avg Difficulty: 0")
            self.grid.addWidget(self.avgdifficulty, 2, 0)
            
            self.avghashrate = QLabel("Avg Hashrate: 0kH/s")
            self.grid.addWidget(self.avghashrate, 2, 1)
    
            self.blockno = QLabel("Block: 0")
            self.grid.addWidget(self.blockno, 2, 2)
    
            addr = QLabel("Address (User)")
            self.nameselect = QLineEdit()
            self.grid.addWidget(addr, 3, 0)
            self.grid.addWidget(self.nameselect, 3, 1, 1, 2)
    
            pool = QLabel("Pool (stratum)")
            self.poolselect = QLineEdit()
            self.grid.addWidget(pool, 4, 0)
            self.grid.addWidget(self.poolselect, 4, 1, 1, 2)
    
            algo = QLabel("Algorithm")
            self.algoselect = QLineEdit("allium")
            self.grid.addWidget(algo, 5, 0)
            self.grid.addWidget(self.algoselect, 5, 1, 1, 2)
    
            intensity = QLabel("Intensity")
            self.intselect = QSpinBox()
            self.intselect.setMinimum(0)
            self.intselect.setMaximum(26)
            self.intselect.setValue(26)
            self.grid.addWidget(intensity, 6, 0)
            self.grid.addWidget(self.intselect, 6, 1, 1, 2)
    
            gap = QLabel("Lookup Gap")
            self.gapselect = QSpinBox()
            self.gapselect.setMinimum(0)
            self.gapselect.setMaximum(10)
            self.gapselect.setValue(2)
            self.grid.addWidget(gap, 7, 0)
            self.grid.addWidget(self.gapselect, 7, 1, 1, 2)
    
            temp = QLabel("Max Temp")
            self.tempselect = QSpinBox()
            self.tempselect.setValue(80)
            self.tempselect.setMinimum(0)
            self.grid.addWidget(temp, 8, 0)
            self.grid.addWidget(self.tempselect, 8, 1, 1, 2)
    
            self.sbutton = QPushButton("Start")
            self.sbutton.clicked.connect(self.startminer)
            self.grid.addWidget(self.sbutton, 9, 1)
    
            self.cbutton = QPushButton("Stop")
            self.cbutton.clicked.connect(self.cancelminer)
            self.grid.addWidget(self.cbutton, 9, 2)
    
        def startminer(self):
            try:
                if self.thread is None:
                    cmd = fmtcmd(user=self.nameselect.text(),
                                 pool=self.poolselect.text(),
                                 algo=self.algoselect.text(),
                                 maxtemp=self.tempselect.value(),
                                 lookupgap=self.gapselect.value(),
                                 intensity=self.intselect.value())
                    self.thread = RunnerThread(self, cmd)
                    self.thread.start()
            except:
                import traceback
                traceback.print_exc()
    
        def cancelminer(self):
            if self.thread is not None:
                self.thread.cancelled = True
                self.thread = None
    
        
    if __name__ == "__main__":
        App().exec()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
