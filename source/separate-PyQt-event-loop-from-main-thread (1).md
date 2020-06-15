---
title: separate PyQt event loop from main thread (1)
date: 2020-05-07
---
Example Python program separate-PyQt-event-loop-from-main-thread (1).py
This program creates a PyQt GUI

## Modules

* import logging
* import threading
* import sys
* import time
* from PyQt5.QtCore import QRect
* from PyQt5.QtWidgets import (QApplication, QWidget)

## Classes

* class MainWindow(QWidget):

## Methods

* 	def __init__(self):
* def ui_thread(app):

## Code

Example Python PyQt program :

    """
    This sample shows how to separate QApplication event loop from main thread.
    This method works only on Linux. On Windows, you will see this app's window freezing.
    """
    import logging
    import threading
    import sys
    import time
    from PyQt5.QtCore import QRect
    from PyQt5.QtWidgets import (QApplication, QWidget)
    
    #logging settings
    logger = logging.getLogger(__name__); logger.setLevel(logging.DEBUG)	#output DEBUG or higher level messages
    handler = logging.StreamHandler(); handler.setLevel(logging.DEBUG)
    handler.setFormatter(logging.Formatter('%(asctime)s - %(name)s - %(threadName)s - %(levelname)s: %(message)s'))
    logger.addHandler(handler)
    
    class MainWindow(QWidget):
    	"""main window class"""
    	def __init__(self):
    		super().__init__()
    		self.setWindowTitle('Main Window')
    		self.setGeometry(QRect(300,300, 200,150))
    
    def ui_thread(app):
    	"""a thread for QApplication event loop"""
    	logger.debug("I'm UI thread.")
    	app[0] = QApplication(sys.argv)
    	app[0].exec_()
    
    if __name__ == '__main__':
    	logger.debug("I'm main thread.")
    
    	#Qreate QApplication instance and start event loop.
    	app = [None]
    	ui_th = threading.Thread(target=ui_thread, args=(app,))
    	ui_th.start()
    	time.sleep(0.05)	#Wait for a short time to ensure QApplication instance created.
    
    	#From now, you can do anything you like!
    	w = MainWindow()
    	w.show()
    
    	time.sleep(1.5)
    	w.setGeometry(QRect(300,300, 400,300))
    	w.setWindowTitle("Size changed!")
    
    	time.sleep(1.5)
    	w.setWindowTitle("Title changed!!!!!!!!!!!!!!!!!!!!!!!!!!!")
    
    	time.sleep(2)
    	app[0].quit()	#end UI thread
    	quit()	#end main thread

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
