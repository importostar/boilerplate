---
title: SimpleGUI
date: 2020-05-07
---
Example Python program SimpleGUI.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import math
* import sys
* import numpy
* from PyQt5.QtCore import *
* from PyQt5.QtGui import *
* from PyQt5.QtWidgets import *

## Classes

* class AppGUI(QMainWindow):
* class HomeLayout(QGridLayout):
* class FirstLayout(QGridLayout):
* class SecondLayout(QGridLayout):

## Methods

* def __init__(self):
* def initLayout(self):
* def initMenuBar(self):
* def initStatusBar(self):
* def closeEvent(self, event):
* def toggleLayout(self):
* def __init__(self):
* def initLayout(self):
* def __init__(self):
* def initLayout(self):
* def checkAns(self):
* def calibProg(self):
* def __init__(self):

## Code

Example Python PyQt program :

    import math
    import sys
    
    import numpy
    from PyQt5.QtCore import *
    from PyQt5.QtGui import *
    from PyQt5.QtWidgets import *
    
    
    #####################################################################
    #      The main GUI of Application inherited from QGridLayout       #
    #####################################################################
    class AppGUI(QMainWindow):
        # initialize the core components of the UI
        def __init__(self):
            # return the parent to AppGUI class
            super().__init__()
            # set up the application menu and status bar
            self.initMenuBar()
            self.initStatusBar()
            # set up the layout of the main window
            self.initLayout()
            # configure the application GUI
            self.resize(1024, 576)
            rect_frame = self.frameGeometry()
            # get the screen resolution to to locate its center point
            center_point = QDesktopWidget().availableGeometry().center()
            rect_frame.moveCenter(center_point)
            # set the top left of the app window to that of the rectangle
            self.move(rect_frame.topLeft())
            self.setWindowTitle('SimpleGUI Application')
            self.setWindowIcon(QIcon('AppIcon.png'))
            self.show()
    
        # initilize the layout for the homepage
        def initLayout(self):
            # create a widget to insert the layout into the main window
            widget_home = QWidget()
            # initilize the application layout from the HomeLayout class
            self.layout = HomeLayout()
            self.layout.btn_select.clicked.connect(self.toggleLayout)
            # add the home layout as the central widget
            widget_home.setLayout(self.layout)
            self.setCentralWidget(widget_home)
            self.progress_bar.reset()
    
        # initialize the menubar containing the new and exit options
        def initMenuBar(self):
            # create a menubar widget and associate a file menu
            menu_bar_main = self.menuBar()
            file_menu_main = menu_bar_main.addMenu('&File')
    
            # create the new option in the file menu
            action_new = QAction(QIcon('NewIcon.png'), '&New', self)
            action_new.setShortcut('Ctrl+N')
            action_new.setStatusTip('Start a new instance of the application.')
            # bind the event to the initLayout handler
            action_new.triggered.connect(self.initLayout)
            file_menu_main.addAction(action_new)
    
            # create the exit option in the file menu
            action_exit = QAction(QIcon('ExitIcon.png'), '&Exit', self)
            action_exit.setShortcut('Ctrl+Q')
            action_exit.setStatusTip('Exit the application.')
            # bind the event to the closeEvent handler
            action_exit.triggered.connect(self.close)
            file_menu_main.addAction(action_exit)
    
        # initialize the status bar to display tips and progress
        def initStatusBar(self):
            # create a statusbar widget
            self.statusBar().showMessage('Welcome.')
            # append a progress bar to the status bar
            self.progress_bar = QProgressBar()
            self.statusBar().addPermanentWidget(self.progress_bar)
            # status_main.setFont(QFont('SansSerif', 9))
            self.setStatusTip('Ready.')
    
        # reimplement the event handler to modify the action of QCloseEvent
        def closeEvent(self, event):
            # display a dialog box before exiting the application
            response = QMessageBox.question(
                self, 'Exit Application', 'Are you sure you want to quit?', QMessageBox.Yes | QMessageBox.No, QMessageBox.No)
            # take action according to the response
            if response == QMessageBox.Yes:
                event.accept()
            else:
                event.ignore()
    
        # toggle layout on button click in the home page
        def toggleLayout(self):
            # conditional toggle upon selection
            if self.layout.combo.currentText() == 'FirstLayout':
                # display the first layout
                widget = QWidget()
                layout = FirstLayout()
                widget.setLayout(layout)
                self.setCentralWidget(widget)
                self.progress_bar.reset()
            elif self.layout.combo.currentText() == 'SecondLayout':
                # display the second layout
                widget = QWidget()
                layout = SecondLayout()
                widget.setLayout(layout)
                self.setCentralWidget(widget)
                self.progress_bar.reset()
    
    #####################################################################
    #           Layout of Homepage inherited from QGridLayout           #
    #####################################################################
    
    
    class HomeLayout(QGridLayout):
        # initialize the super class and the call the layout method
        def __init__(self):
            super().__init__()
            self.setSpacing(5)
            self.initLayout()
    
        # initialize the components of the layout
        def initLayout(self):
            # initialize the combo box for layout selection
            self.label_select_layout = QLabel('Select the Layout to display: ')
            self.label_select_layout.resize(self.label_select_layout.sizeHint())
            self.combo = QComboBox()
            self.combo.addItems(['FirstLayout', 'SecondLayout'])
            self.combo.setCurrentIndex(0)
            self.addWidget(self.label_select_layout, 0, 0)
            self.addWidget(self.combo, 0, 1)
    
            # create button to execute desired selection
            self.btn_select = QPushButton('Select')
            self.btn_select.setStatusTip(
                'Click the button to display the selected layout.')
            self.btn_select.resize(self.btn_select.sizeHint())
            self.addWidget(self.btn_select, 1, 1)
    
    #####################################################################
    #    			      First Layout inherited from QGridLayout     		    #
    #####################################################################
    
    
    class FirstLayout(QGridLayout):
        # initialize the super class and call the layout method
        def __init__(self):
            super().__init__()
            self.setSpacing(5)
            self.initLayout()
    
        # initialize the layout
        def initLayout(self):
            # an entry field
            self.val_pi = QLineEdit()
            self.val_pi.setText('3.14159')
            self.addWidget(
                QLabel('Enter the value of Pi rounded to 5 decimal places: '), 0, 0)
            self.addWidget(self.val_pi, 0, 1)
            self.val_pi.setText('3.14159')
    
    		# a combo box
            self.sel_pi = QComboBox()
            self.sel_pi.addItems(['3.14157', '3.14158', '3.14159', '3.14286'])
            self.addWidget(
                QLabel('Select the value of Pi rounded to 5 decimal places: '), 2, 0)
            self.addWidget(self.sel_pi, 2, 1)
    
           	# a push button to check the answers of the form
            self.btn_check = QPushButton('Check Answers')
    		# display status tip on hover
            self.btn_check.setStatusTip(
                'Click on the button to check the answers.')
            self.btn_check.resize(self.btn_check.sizeHint())
    		# execute a function on click
            self.btn_check.clicked.connect(self.checkAns)
            self.addWidget(self.btn_check, 3, 1)
    
           	# a push button to calibrate progress bar
            self.btn_calib = QPushButton('Calibrate Progress Bar')
    		# display status tip on hover
            self.btn_calib.setStatusTip(
                'Click on the button to calibrate the progress bar.')
            self.btn_calib.resize(self.btn_calib.sizeHint())
    		# execute a function on click
            self.btn_calib.clicked.connect(self.calibProg)
            self.addWidget(self.btn_calib, 4, 1)
    
        def checkAns(self):
            gui.statusBar().showMessage('Checking the answers...')
            # initialize the x-axis variation type
            if self.sel_pi.currentIndex() == 2 and self.val_pi.text() == '3.14159':
                gui.statusBar().showMessage('Correct Answer!')
                print('Correct Answer!')
            else:
                gui.statusBar().showMessage('Wrong Answer!')
                print('Wrong Answer!')
            self.calibProg()
            
        def calibProg(self):
            gui.statusBar().showMessage('Calibrating the progress bar...')
            # iterate over various values
            for i in range(1, int(1000)):
                gui.progress_bar.setValue(float(i/10))
                gui.statusBar().showMessage('Iteration #' + str(i) + '.')
                
            # reset the progress bar
            gui.progress_bar.reset()
            gui.statusBar().showMessage('Done.')
            
    #####################################################################
    #    			    Second Layout inherited from QGridLayout      		    #
    #####################################################################
    class SecondLayout(QGridLayout):
        # initialize the super class and call the layout method
        def __init__(self):
            super().__init__()    
    
    # run the main loop of the application
    if __name__ == '__main__':
        # create application object with command line arguments
        app = QApplication(sys.argv)
        gui = AppGUI()
        # initiate the main loop
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
