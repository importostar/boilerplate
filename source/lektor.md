---
title: lektor
date: 2020-05-07
---
Example Python program lektor.py
This program creates a PyQt GUI

## Modules

* import atexit
* import os
* import sys
* from PyQt5.QtCore import QTimer, pyqtSignal, QProcess, QUrl
* from PyQt5.QtGui import QTextCursor, QDesktopServices
* from PyQt5.QtWidgets import (
* import frozen_stubs

## Classes

* class MainWindow(QMainWindow):

## Methods

* def __init__(self):
* def open_site(self):
* def open_admin(self):
* def lookup_lektor(self):
* def append_data(self, data):
* def read_proc(self):
* def finish_proc(self):
* def open_click(self):
* def update_button_state(self):
* def proc_kill(self):
* def app_main(args):

## Code

Example Python PyQt program :

    import atexit
    import os
    import sys
    
    from PyQt5.QtCore import QTimer, pyqtSignal, QProcess, QUrl
    from PyQt5.QtGui import QTextCursor, QDesktopServices
    from PyQt5.QtWidgets import (
        QApplication,
        QHBoxLayout,
        QMainWindow,
        QMessageBox,
        QPlainTextEdit,
        QPushButton,
        QVBoxLayout,
        QWidget,
        QFileDialog,
    )
    
    import frozen_stubs
    
    
    class MainWindow(QMainWindow):
        def __init__(self):
            super().__init__()
            self.resize(400, 150)
            self.setWindowTitle('Lektor')
    
            self.setCentralWidget(QWidget())
            self.centralWidget().setLayout(QVBoxLayout())
    
            layout = self.centralWidget().layout()
            button_container = QWidget(self.centralWidget())
            button_container.setLayout(QHBoxLayout())
            layout.addWidget(button_container)
            self.log = QPlainTextEdit(self.centralWidget())
            layout.addWidget(self.log)
    
            layout = button_container.layout()
            self.open_button = QPushButton('Open', button_container)
            self.open_button.clicked.connect(self.open_click)
            layout.addWidget(self.open_button)
    
            self.close_button = QPushButton('Close', button_container)
            self.close_button.setEnabled(False)
            self.close_button.clicked.connect(self.proc_kill)
            layout.addWidget(self.close_button)
    
            self.browse_button = QPushButton('Browse', button_container)
            self.browse_button.setEnabled(False)
            self.browse_button.clicked.connect(self.open_site)
            layout.addWidget(self.browse_button)
    
            self.admin_button = QPushButton('Admin', button_container)
            self.admin_button.setEnabled(False)
            self.admin_button.clicked.connect(self.open_admin)
            layout.addWidget(self.admin_button)
    
            self.proc = None
            self.update_button_state()
    
        def open_site(self):
            QDesktopServices.openUrl(QUrl('http://127.0.0.1:5000'))
    
        def open_admin(self):
            QDesktopServices.openUrl(QUrl('http://127.0.0.1:5000/admin'))
    
        def lookup_lektor(self):
            meipass = getattr(sys, '_MEIPASS', None)
            script = meipass or __file__
            script_dir = os.path.dirname(os.path.abspath(script))
            if meipass:
                script_dir = os.path.join(script_dir, 'Resources')
            lektor = os.path.join(script_dir, 'lektor.pex')
            if not os.path.exists(lektor):
                lektor = None
            return lektor
    
    
        def append_data(self, data):
            self.log.moveCursor(QTextCursor.End)
            self.log.insertPlainText(data)
            self.log.moveCursor(QTextCursor.End)
    
        def read_proc(self):
            self.append_data(bytes(self.proc.readAllStandardOutput()).decode())
            self.append_data(bytes(self.proc.readAllStandardError()).decode())
    
        def finish_proc(self):
            self.read_proc()
            self.proc = None
            self.update_button_state()
    
        def open_click(self):
            if self.proc:
                self.proc_kill()
            lektor = self.lookup_lektor()
            if lektor is None:
                QMessageBox.critical(self, self.windowTitle(), 'Lektor binary not found')
                return
            file_name, _ = QFileDialog.getOpenFileName(
                self,
                'Open project',
                filter='Project Files (*.lektorproject)'
            )
            if not file_name:
                return
            self.proc = QProcess(self)
            self.proc.readyRead.connect(self.read_proc)
            self.proc.start(' '.join([
                lektor,
                '--project',
                os.path.dirname(file_name),
                'server',
                '-p',
                '5000',
            ]))
            self.proc.finished.connect(self.finish_proc)
            self.update_button_state()
    
        def update_button_state(self):
            self.close_button.setEnabled(self.proc is not None)
            self.browse_button.setEnabled(self.proc is not None)
            self.admin_button.setEnabled(self.proc is not None)
            self.log.setVisible(self.proc is not None)
    
        def proc_kill(self):
            if self.proc is not None:
                self.proc.kill()
                self.log.clear()
            self.update_button_state()
    
    
    def app_main(args):
        app = QApplication(sys.argv)
        win = MainWindow()
        win.show()
        try:
            atexit.register(win.proc_kill)
            return app.exec_()
        finally:
            atexit.unregister(win.proc_kill)
            win.proc_kill()
    
    
    if __name__ == '__main__':
        sys.exit(app_main(sys.argv))
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
