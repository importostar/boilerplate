---
title: PyQtDemo
date: 2020-05-07
---
Example Python program PyQtDemo.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtCore import *
* from PyQt5.QtWidgets import *
* import sys
* # This line is so important cuz if you dont show() it wont show a thing.

## Classes

* class Home(QWidget):

## Methods

* def __init__(self, parent=None):

## Code

Example Python PyQt program :

    '''
    First you will need to install qt5 on your system,
    for that you will need to do this in you terminal:
        sudo apt-get qt5-default
        and then,
        pip install sip PyQt5
    '''
    from PyQt5.QtCore import *
    from PyQt5.QtWidgets import *
    
    
    # Create a HomePage for our Qtapp
    class Home(QWidget):
        def __init__(self, parent=None):
            super(Home, self).__init__(parent)
    
            # Lets create a label to display in our app
            label = QLabel('Sanket Gadge')
    
            # Lets create a layout for our app
            layout = QVBoxLayout()
    
            # Add our label to this layout
            layout.addWidget(label)
    
            # Once we have everything set up, we have all our widgets and layouts created its time to set the layout for our app.
            self.setLayout(layout)
            # Then we give name to a window to show our widgets and layout
            self.setWindowTitle("My QT app")
    
    
    # Once we have our class created its time to call it
    if __name__ == '__main__':
        import sys
    
        # Define a name for our app
        app = QApplication(sys.argv)
    
        # Call the class object we have created earlier
        window = Home()
        # This line is so important cuz if you dont show() it wont show a thing.
        window.show()
    
        # When user wants to exit, it will raise a exit call for our app, this will run when you press the close mark(beside minimize button)in the app window
        sys.exit(app.exec_())    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
