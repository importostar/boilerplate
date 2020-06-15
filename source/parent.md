---
title: parent
date: 2020-05-07
---
Example Python program parent.py
This program creates a PyQt GUI

## Modules

* import sys
* import time
* import Queue
* import threading
* import subprocess
* import contextlib
* from PyQt5 import QtWidgets, QtCore

## Classes

* class Parent(QtWidgets.QWidget):

## Methods

* def __init__(self, to_queue, from_queue, parent=None):
* def send(self):
* def run(self, command):
* def listen(self):
* def writer(f, queue):
* def reader(f, queue):
* def application():

## Code

Example Python PyQt program :

    import sys
    import time
    import Queue
    import threading
    import subprocess
    import contextlib
    
    from PyQt5 import QtWidgets, QtCore
    
    
    class Parent(QtWidgets.QWidget):
        appended = QtCore.pyqtSignal(str)
    
        def __init__(self, to_queue, from_queue, parent=None):
            super(Parent, self).__init__(parent)
            self.setWindowTitle("Parent")
            self.setFixedSize(400, 500)
    
            output = QtWidgets.QPlainTextEdit()
            edit = QtWidgets.QLineEdit()
    
            output.setReadOnly(True)
    
            layout = QtWidgets.QVBoxLayout(self)
            layout.addWidget(output)
            layout.addWidget(edit)
    
            edit.setFocus()
    
            # Signals
            edit.returnPressed.connect(self.send)
            self.appended.connect(output.appendPlainText)
    
            # References
            self.edit = edit
            self.output = output
            self.to_queue = to_queue
            self.from_queue = from_queue
    
            threading.Thread(target=self.listen).start()
    
        def send(self):
            command = self.edit.text()
    
            if not command:
                return
    
            self.to_queue.put("request:" + command)
            self.edit.clear()
    
        def run(self, command):
            if command == "update":
                self.appended.emit("Update requested..")
                time.sleep(1)
    
                result = list()
                for i in range(10):
                    result.append("%d" % i)
    
                self.appended.emit("Sending items..")
                self.to_queue.put("response:update|" + "\\".join(result))
                self.appended.emit("Items sent successfully")
    
        def listen(self):
            for line in iter(self.from_queue.get, None):
                self.appended.emit("> %s" % line)
    
                topic, contents = line.split(":", 1)
    
                if topic == "request":
                    self.run(contents)
    
    
    def writer(f, queue):
        """Send to file-like object
    
        Arguments:
            f (file): Channel through which to send
            queue (Queue.Queue): Plain-text to send
    
        """
    
        for line in iter(queue.get, None):
            f.write(line + "\n")
        f.close()
    
    
    def reader(f, queue):
        """Read from file-like object
    
        Arguments:
            f (file): Channel from which to read
            queue (Queue): Store output here
    
        """
    
        for line in iter(f.readline, b""):
            queue.put(line.rstrip())
        f.close()
    
    
    @contextlib.contextmanager
    def application():
        app = QtWidgets.QApplication(sys.argv)
        yield
        app.exec_()
    
    
    if __name__ == '__main__':
        process = subprocess.Popen(["python", "-u", "child.py"],
                                   stdout=subprocess.PIPE,
                                   stdin=subprocess.PIPE)
        to_queue = Queue.Queue()
        from_queue = Queue.Queue()
    
        threading.Thread(target=writer, args=[process.stdin, to_queue]).start()
        threading.Thread(target=reader, args=[process.stdout, from_queue]).start()
    
        with application():
            window = Parent(to_queue, from_queue)
            window.show()
    
        # Cleanup threads
        to_queue.put(None)
        from_queue.put(None)
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
