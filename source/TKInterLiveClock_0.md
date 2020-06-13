---
title: TKInterLiveClock_0
date: 2020-05-07
---
Example Python program TKInterLiveClock_0.py

## Modules

* from Tkinter import *  # Python 2
* # from tkinter import *  # Python 3
* import datetime
* import threading

## Classes

* class Clock(Frame):

## Methods

* def __init__(self, master):
* def start(self):
* def stop(self):
* def update(self):

## Code

Python tkinter example

    from Tkinter import *  # Python 2
    # from tkinter import *  # Python 3
    
    
    import datetime
    import threading
    
    class Clock(Frame):
        def __init__(self, master):
            Frame.__init__(self, master)
            
            self.updating = BooleanVar()
            
            self.ValueHour = IntVar()
            self.LabelHour = Label(self)
            self.LabelHour.grid(row=0, column=0)
            self.LabelHourUpdate = Label(self, textvariable=self.ValueHour)
            self.LabelHourUpdate.grid(row=0, column=1)
            
            self.ValueMinute = IntVar()
            self.LabelMinute = Label(self)
            self.LabelMinute.grid(row=1, column=0)
            self.LabelMinuteUpdate = Label(self, textvariable=self.ValueMinute)
            self.LabelMinuteUpdate.grid(row=1, column=1)
            
            self.ValueSecond = IntVar()
            self.LabelSecond = Label(self)
            self.LabelSecond.grid(row=2, column=0)
            self.LabelSecondUpdate = Label(self, textvariable=self.ValueSecond)
            self.LabelSecondUpdate.grid(row=2, column=1)
            
            self.btn_start = Button(self, text="Start", command=self.start)
            self.btn_start.grid(row=3, column=0)
            
            self.btn_stop = Button(self, text="Stop", command=self.stop)
            self.btn_stop.grid(row=3, column=1)
            
        def start(self):
            if not self.updating.get():
                self.updating.set(True)
                self.new_thread = threading.Thread(target=self.update)
                self.new_thread.start()
            
        def stop(self):
            self.updating.set(False)
            
        def update(self):
            while self.updating.get():
                now = datetime.datetime.now()
                self.ValueHour.set(now.hour)
                self.ValueMinute.set(now.minute)
                self.ValueSecond.set(now.second)
                
    root = Tk()
    clock = Clock(root)
    clock.pack()
    root.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
