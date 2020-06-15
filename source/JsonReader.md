---
title: JsonReader
date: 2020-05-07
---
Example Python program JsonReader.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5.QtWidgets import QApplication, QWidget, QInputDialog, QLineEdit, QPushButton
* from PyQt5.QtGui import QIcon
* from PyQt5.QtCore import pyqtSlot
* import sys
* import json
* import sched, time

## Classes

* class App(QWidget):

## Methods

* def __init__(self):
* def initUI(self):
* def the_thing(self):
* def on_click(self):

## Code

Example Python PyQt program :

    from PyQt5.QtWidgets import QApplication, QWidget, QInputDialog, QLineEdit, QPushButton
    from PyQt5.QtGui import QIcon
    from PyQt5.QtCore import pyqtSlot
    import sys
    import json
    import sched, time
    
    s = sched.scheduler(time.time, time.sleep)
    
    # opens the playback json file in Google Music for Desktop
    # Grabs the data from the dictionary and saves them to variables
    with open('playback.json') as data:
        jsondata = json.load(data)
        songtitle = jsondata['song']['title']
        artist = jsondata['song']['artist']
        album = jsondata['song']['album']
    
    
    #PyQt5 app setup
    class App(QWidget):
            def __init__(self):
                super().__init__()
                self.title = 'Json to Text Widget'
                self.left = 75
                self.top = 75
                self.width = 420
                self.height = 120
                self.initUI()
    
    #Creates main window, creates textbox requesting frequency (in minutes) app grabs data from json
            def initUI(self):
                self.setWindowTitle(self.title)
                self.setGeometry(self.left, self.top, self.width, self.height)
                self.textbox = QLineEdit(self)
                self.textbox.move(20,20)
                self.textbox.resize(280,40)
                button = QPushButton('How often should this run?', self)
                button.setToolTip('Butts is not a valid integer')
                button.move(100, 70)
                button.clicked.connect(self.on_click)
    
                self.show()
    
            def the_thing(self):
                s.enter(textboxValue, 1, the_thing(self))
                with open('playback.json') as data:
                    jsondata = json.load(data)
                    songtitle = jsondata['song']['title']
                    artist = jsondata['song']['artist']
                    album = jsondata['song']['album']
                    data.close()
                with open('playlist.txt', 'w') as playlist:
                    playlist.write('{0} by {1} from album: {2}\n'.format(songtitle, artist, album))
                    playlist.close()
    # button press. Grabs data from text box, opens playlist.txt as write, then pastes data in user-friendly format
    # Prints to console frequency app will run.
            @pyqtSlot()
            def on_click(self):
                textboxValue = self.textbox.text()
                with open('playlist.txt', 'w') as playlist:
                    playlist.write('{0} by {1} from album: {2}\n'.format(songtitle, artist, album))
                    playlist.close()
                    print('Currently running every ' + textboxValue + ' minutes')
    
    
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        ex = App()
        sys.exit(app.exec_())
    
    # Overall goal is to have the app grab json every X minutes (X = user input) and then paste them into a text file
    # that OBS will then read.
    # TODO Figure out how to set the app to run X minutes
    # TODO NOTE ABOVE - Don't forget to re-open the JSON file every loop. Currently it's not setup to do that
    # TODO Print frequency app will run in-message box.
    
    
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
