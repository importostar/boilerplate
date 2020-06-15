---
title: mergin_gui2
date: 2020-05-07
---
Example Python program mergin_gui2.py
This program creates a PyQt GUI

## Modules

* import os
* from PyQt5.QtCore import QTimer
* from PyQt5.QtWidgets import QWidget, QVBoxLayout, QProgressBar, QApplication, QPushButton, QLabel, QMessageBox
* from mergin import (
* from mergin.client_pull import download_project_async, download_project_is_running, download_project_finalize, download_project_cancel

## Classes

* class MyWidget(QWidget):

## Methods

* def __init__(self, parent=None):
* def start_download(self):
* def timer_timeout(self):
* def cancel_download(self):

## Code

Example Python PyQt program :

    
    import os
    
    from PyQt5.QtCore import QTimer
    from PyQt5.QtWidgets import QWidget, QVBoxLayout, QProgressBar, QApplication, QPushButton, QLabel, QMessageBox
    
    from mergin import (
        MerginClient,
        MerginProject,
        InvalidProject,
        ClientError,
    )
    
    from mergin.client_pull import download_project_async, download_project_is_running, download_project_finalize, download_project_cancel
    
    # config
    project = "martin/fibre"
    mergin_user = "martin"
    mergin_pass = "xxx"
    c = MerginClient("https://public.cloudmergin.com/", None, mergin_user, mergin_pass)
    directory = os.path.basename(project)
    
    
    app = QApplication([])
    
    class MyWidget(QWidget):
        def __init__(self, parent=None):
            QWidget.__init__(self, parent)
            
            self.bar = QProgressBar(self)
            self.status_label = QLabel(self)
            self.start_button = QPushButton(self)
            self.start_button.setText("Start!")
            self.cancel_button = QPushButton(self)
            self.cancel_button.setText("Cancel!")
            
            main_layout = QVBoxLayout()
            main_layout.addWidget(self.bar)
            main_layout.addWidget(self.status_label)
            main_layout.addWidget(self.start_button)
            main_layout.addWidget(self.cancel_button)
            self.setLayout(main_layout)
            
            self.timer = QTimer(self)
            self.timer.setInterval(100)
            
            self.start_button.clicked.connect(self.start_download)
            self.cancel_button.clicked.connect(self.cancel_download)
            self.timer.timeout.connect(self.timer_timeout)
            
            self.job = None
    
        def start_download(self):
            if self.job:
                QMessageBox.information(self, "msg", "already downloading")
                return
            try:
                self.job = download_project_async(c, project, directory)
            except ClientError as e:
                QMessageBox.critical(self, "msg", "Client error: " + str(e))
                return
    
            self.status_label.setText("downloading!")
            self.bar.setMaximum(self.job.total_size)
            self.bar.setValue(0)
            self.timer.start()
            
        def timer_timeout(self):
            self.bar.setValue(self.job.transferred_size)
            
            try:
                is_running = download_project_is_running(self.job)
            except ClientError as e:
                # also try to cancel the job so that we do not need to wait for other workers
                self.cancel_download()
                self.status_label.setText("error!")
                QMessageBox.critical(self, "msg", "Client error: " + str(e))
                return
    
            if not is_running:
                self.timer.stop()
                try:
                    # this should not raise an exception anymore because we were signalled that
                    # all workers have finished successfully. But maybe something in finalization could fail (e.g. disk full?)
                    download_project_finalize(self.job)
                except ClientError as e:
                    self.job = None
                    self.status_label.setText("error!")
                    QMessageBox.critical(self, "msg", "Client error: " + str(e))
                    return
    
                self.job = None
                self.status_label.setText("")
                QMessageBox.information(self, "msg", "DONE!")
            
        def cancel_download(self):
            if not self.job:
                QMessageBox.information(self, "msg", "download not active")
                return
            self.timer.stop()
            self.status_label.setText("cancelled!")
            download_project_cancel(self.job)
            self.job = None
    
    
    w = MyWidget()
    w.show()
    app.exec_()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
