---
title: output_redirect
date: 2020-05-07
---
Example Python program output_redirect.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import time
* from multiprocessing import Pipe, Process
* from PyQt5.QtCore import QThread, QMetaObject, Q_ARG
* from PyQt5.QtWidgets import *

## Classes

* class PipeOutput(object):
* class TextEditDispatcher(QThread):

## Methods

* def __init__(self, pipe):
* def write(self, s):
* def flush(self):
* def print_name(pipe, name):
* def __init__(self):
* def add_connection(self, widget, pipe):
* def run(self):

## Code

Example Python PyQt program :

    #!/usr/bin/env python3
    import sys
    import time
    from multiprocessing import Pipe, Process
    from PyQt5.QtCore import QThread, QMetaObject, Q_ARG
    from PyQt5.QtWidgets import *
    
    # Example is a quite ugly, but works
    
    class PipeOutput(object):
        def __init__(self, pipe):
            self.pipe = pipe
        def write(self, s):
            self.pipe.send(s)
        def flush(self):
            pass
    
    def print_name(pipe, name):
        sys.stdout = PipeOutput(pipe)
        while True:
            print('Process name: ' + name)
            time.sleep(0.5)
    
    
    class TextEditDispatcher(QThread):
        def __init__(self):
            QThread.__init__(self)
            self.connections = []
    
        def add_connection(self, widget, pipe):
            self.connections.append((widget, pipe))
    
        def run(self):
            while (True):
                for widget, pipe in self.connections:
                    if pipe.poll():
                        text = pipe.recv().strip()
                        QMetaObject.invokeMethod(widget, 'append', Q_ARG(str, text))
    
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        window = QSplitter()
        out_a = QTextEdit()
        out_b = QTextEdit()
        window.addWidget(out_a)
        window.addWidget(out_b)
        window.show()
    
        cna_recv, cna_send = Pipe(False)
        cnb_recv, cnb_send = Pipe(False)
    
        proc_a = Process(target=print_name, args=(cna_send, 'Alice'))
        proc_b = Process(target=print_name, args=(cnb_send, 'Bob'))
    
        proc_a.start()
        proc_b.start()
    
        dsp = TextEditDispatcher()
        dsp.add_connection(out_a, cna_recv)
        dsp.add_connection(out_b, cnb_recv)
        dsp.start()
    
        ret = app.exec_()
        proc_a.terminate()
        proc_b.terminate()
        sys.exit(ret)
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
