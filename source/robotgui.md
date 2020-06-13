---
title: robotgui
date: 2020-05-07
---
Example Python program robotgui.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter
* import sys
* import tfun

## Methods

* def main():
* def quitHandler():
* def sensorHandler():

## Code

Python tkinter example

    import tkinter
    import sys
    import tfun
    
    
    def main():
        root = tkinter.Tk()
        root.title("ROBOT GUI")
    
       
        #frame=tkinter.Frame(root)
        #frame.pack(side=tkinter.RIGHT, fill=tkinter.BOTH)
    
        sensorLab=tkinter.Label(root, text="Sensor", bg="blue", width=20, fg="white")
        sensorLab.grid(row=1,column=0, sticky="w")
    
        servoLab=tkinter.Label(root, text="Servo", bg="blue", fg="Pink", width=20)
        servoLab.grid(row=1, column=1)
    
        motorLab=tkinter.Label(root, text="motor", bg="blue", fg="white", width=20)
        motorLab.grid(row=1, column=2)
    
        lightLab=tkinter.Label(root, text="Lights", bg="blue", fg="white", width=20)
        lightLab.grid(row=1, column=3)
        
        servoButtonl=tkinter.Button(root, text="Servo Full Left", width=20)
        servoButtonl.grid(row=2, column=1)
        servoButtonm=tkinter.Button(root, text="Servo Middle", width=20)
        servoButtonm.grid(row=3, column=1)
        servoButtonr=tkinter.Button(root, text="Servo Full Right", width=20)
        servoButtonr.grid(row=4, column=1)
    
    
        motorButtonfw=tkinter.Button(root, text="Forward", width=20)
        motorButtonfw.grid(row=2, column=2)
    
        motorButtonrv=tkinter.Button(root, text="Reverse", width=20)
        motorButtonrv.grid(row=3, column=2)
    
        motorButtonpl=tkinter.Button(root, text="Pivot Left", width=20)
        motorButtonpl.grid(row=4, column=2)
        
        motorButtonpr=tkinter.Button(root, text="Pivot Right", width=20)
        motorButtonpr.grid(row=5, column=2)
    
        lightButtonon=tkinter.Button(root, text="Lights On", width=20)
        lightButtonon.grid(row=2,column=3)
    
        lightButtonoff=tkinter.Button(root, text="Lights Off", width=20)
        lightButtonoff.grid(row=3,column=3)
    
        cleanupButton=tkinter.Button(root, text="GPIO.cleanup", width=20)
        cleanupButton.grid(row=5, column=0)
    
    
    
        def quitHandler():
            print("quit")
            exit(0)
        quitButton=tkinter.Button(root,text="Quit", command=quitHandler, bg="red", fg="white", width=40)
        quitButton.grid(row=6, column=1, columnspan=2)    
    
    
        def sensorHandler():
            # call sensor distane function
            return
        
        SensorButton=tkinter.Button(root, text="Distance", width=20, command=tfun.tfunc)
        SensorButton.grid(row=2, column=0 )
       
        tkinter.mainloop()
    
    
    
    if __name__ == "__main__":
        main()
        
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
