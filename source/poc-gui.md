---
title: poc gui
date: 2020-05-07
---
Example Python program poc-gui.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter
* import time
* import serial

## Classes

* class gui(tkinter.Tk):

## Methods

* def __init__(self,parent):
* def initialize(self):
* def OnButtonClick(self):
* def OffButtonClick(self):
* def BootedButton(self):

## Code

Python tkinter example

    import tkinter
    import time
    import serial
    
    ser = serial.Serial ('/dev/ttyUSB0',9600) #Used for Pro Mini
    
    class gui(tkinter.Tk):
            def __init__(self,parent):
                    tkinter.Tk.__init__(self,parent)
                    self.parent = parent
                    #ser = serial.Serial ('/dev/ttyACM0',9600)
                    self.initialize()
                    
            def initialize(self):
                    self.grid()
    
                    #self.entry = Tkinter.Entry(self)
                    #self.entry.grid(column=0, row=0, sticky='EW')
                    
                    Label = tkinter.Label(self, text='.          .')
                    Label.grid(column=1, row=0)
    
                    button = tkinter.Button(self, text="Turn LED on!",
                                            command=self.OnButtonClick)
                    button.grid(column=0, row=1)
                    
                    button = tkinter.Button(self, text="Turn LED off!",
                                            command=self.OffButtonClick)
                    button.grid(column=2, row=1)
                    
                    button = tkinter.Button(self, text="Send booted message",
                                            command=self.BootedButton)
                    button.grid(column=3, row=1)
    
    
            def OnButtonClick(self):
                    print("You clicked the ON button!")
                    ser.write("Y")
                    Label = tkinter.Label(self, text='LED ON')
                    Label.grid(column=1, row=0)
            def OffButtonClick(self):
                    print("You clicked the OFF button!")
                    ser.write("N")
                    Label = tkinter.Label(self, text='LED OFF')
                    Label.grid(column=1, row=0)
            def BootedButton(self):
                    print("You clicked the booted button")
                    ser.write("B")
                    Label = tkinter.Label(self, text='Sent Booted msg')
                    Label.grid(column=1, row=0)
                    
    if __name__ == "__main__":
            app = gui(None)
            app.title('Turn LED On & Off')
            app.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
