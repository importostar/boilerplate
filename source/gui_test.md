---
title: gui_test
date: 2020-05-07
---
Example Python program gui_test.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import SmartMotor,tkinter

## Classes

* class GUI(tkinter.Frame):

## Methods

* def __init__(self,master = None):
* def CreateWidgets(self):
* def Funtion_openSerial(self):
* def Funtion_testMotor(self):

## Code

Python tkinter example

    import SmartMotor,tkinter
    
    class GUI(tkinter.Frame):
        def __init__(self,master = None):
           tkinter.Frame.__init__(self,master)
           self.grid()
           self.CreateWidgets()
           
        def CreateWidgets(self):
           self.T_usbPort = tkinter.Label(self)
           self.T_usbPort['text'] = "Usbport"
           self.T_usbPort.grid(row=0,column=0)
           self.F_usbPort = tkinter.Entry(self)
           self.F_usbPort.grid(row=0,column=1,columnspan=6)
                  
           self.T_usbBaudrate = tkinter.Label(self)
           self.T_usbBaudrate['text'] = "Baudrate"
           self.T_usbBaudrate.grid(row=1,column=0)
           self.F_usbBaudrate = tkinter.Entry(self)
           self.F_usbBaudrate.grid(row=1,column=1,columnspan=6)
           
           self.T_MotorNum = tkinter.Label(self)
           self.T_MotorNum['text'] = 'MotorNum'
           self.T_MotorNum.grid(row=2,column=0)
           self.F_MotorNum = tkinter.Entry(self)
           self.F_MotorNum.grid(row=2,column=1,columnspan=6)
                  
           self.openSerial = tkinter.Button(self)
           self.openSerial['text'] = 'Open Serial port'
           self.openSerial.grid(row=3,column=0,columnspan=3)
           self.openSerial['command'] = self.Funtion_openSerial()
           
           self.testMotor = tkinter.Button(self,text = 'testMotor')
           self.testMotor.grid(row=3,column=3,columnspan=3)
           self.testMotor['command'] = self.Funtion_testMotor()
           
        def Funtion_openSerial(self):
           self.M = SmartMotor.SmartMotor(
               _port        = '/dev/ttyUSB0',
               _baudrate    = '9600'
           )
           self.M.setupSerialConnection()
           print('openSerial')
           
        def Funtion_testMotor(self):
           self.M.move_test()
           print('move_test')
                  
    if __name__ == '__main__':
        root = tkinter.Tk()
        app = GUI(master = root)
        app.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
