---
title: child (1)
date: 2020-05-07
---
Example Python program child (1).py
This program creates a PyQt GUI

## Modules

* import sys
* import threading
* import contextlib
* from PyQt5 import QtWidgets, QtCore

## Classes

* class Child(QtWidgets.QWidget):

## Methods

* def __init__(self, parent=None):
* def request_update(self):
* def update(self, items):
* def on_reset(self):
* def run(self, command, args):
* def listen(self):
* def on_append(self, line):
* def send(self, line):
* def application():

## Code

Example Python PyQt program :

    import sys
    import threading
    import contextlib
    
    from PyQt5 import QtWidgets, QtCore
    
    
    class Child(QtWidgets.QWidget):
        appended = QtCore.pyqtSignal(str)
        resetted = QtCore.pyqtSignal()
    
        def __init__(self, parent=None):
            super(Child, self).__init__(parent)
            self.setWindowTitle("Child")
            self.setFixedSize(500, 300)
    
            output = QtWidgets.QPlainTextEdit()
            output.setReadOnly(True)
            button = QtWidgets.QPushButton("Update")
            button.pressed.connect(self.request_update)
    
            layout = QtWidgets.QVBoxLayout(self)
            layout.addWidget(output)
            layout.addWidget(button)
    
            self.thread = threading.Thread(target=self.listen).start()
            self.output = output
    
            self.appended.connect(self.on_append)
            self.resetted.connect(self.on_reset)
    
        def request_update(self):
            """Ask for items from parent"""
            self.on_append("Querying..")
            self.send("request:update")
    
        def update(self, items):
            self.appended.emit("Updating with %s" % str(items))
            self.resetted.emit()
    
        def on_reset(self):
            self.setStyleSheet("")
    
        def run(self, command, args):
            """Run command from parent
    
            Arguments:
                command (str): Command to run
                args (list): Arguments passed to command
    
            """
    
            self.appended.emit("> %s %s" % (command, " ".join(args)))
    
            if command == "changeColor":
                if not args:
                    return self.appended.emit("Expected color in arguments")
    
                self.setStyleSheet("""
    
                QPlainTextEdit {
                    background-color: %s;
                }
    
                """ % args[0])
    
                self.appended.emit("Color changed to \"%s\"" % args[0])
    
            else:
                sys.stderr.write("Command is: %r" % command)
                self.appended.emit("Unknown command: \"%s\"" % command)
    
        def listen(self):
            while True:
                line = sys.stdin.readline()
                if not line:
                    break
    
                # Every line ends with a newline and on
                # Windows a newline + carriage return
                line = line.rstrip()
    
                topic, content = line.split(":", 1)
    
                if topic == "response":
                    command, value = content.split("|")
    
                    if command == "update":
                        self.update(value.split("\\"))
    
                    else:
                        self.appended.emit("Unknown response: \"%s\"" % command)
    
                elif topic == "request":
                    command, args = (content.split(" ", 1) + [None])[:2]
                    self.run(command, args.split() if args else [])
    
                else:
                    self.appended.emit("Unknown input: \"%s\"" % line.rstrip())
    
        def on_append(self, line):
            self.output.appendPlainText(line)
    
        def send(self, line):
            sys.stdout.write(line + "\n")
    
    
    @contextlib.contextmanager
    def application():
        app = QtWidgets.QApplication(sys.argv)
        yield
        app.exec_()
    
    
    if __name__ == '__main__':
        with application():
            window = Child()
            window.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
