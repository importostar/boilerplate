---
title: gui_tkinter
date: 2020-05-07
---
Example Python program gui_tkinter.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys, os, time, datetime
* from pprint import pprint
* import tkinter as tk

## Classes

* class InteractiveTimer(object):
* class App(object):

## Methods

* def __init__( self, name='', period_ms=60*1000, count=-1 ):
* def start( self ):
* def expired(self):
* def __init__(self):
* def update_clock(self):

## Code

Python tkinter example

    #!/bin/python3
    # WARNING -- This code is not thread safe. Google tkinter and thread saftey!
    
    import sys, os, time, datetime
    from pprint import pprint
    
    # Modified from: http://stackoverflow.com/questions/2400262/how-to-create-a-timer-using-tkinter
    import tkinter as tk
    
    class InteractiveTimer(object):
        ''' Simple class to keep track of how much time expired. Does not asyncronously create events/callbacks once time has expired. '''
        instance_count = 0
        def __init__( self, name='', period_ms=60*1000, count=-1 ):
            InteractiveTimer.instance_count = InteractiveTimer.instance_count + 1
            self.id = InteractiveTimer.instance_count
            self.name = name
            if not self.name:
                self.name = "ID_%d" % self.id
            self.period_ms = period_ms
            self.last_query_time = 0
            self.count = count
            self.running = 0
    
        def start( self ):
            if self.running != 0: print( "Error: timer %s was already started" % self.name )
            self.running = 1
            self.last_query_time = datetime.datetime.now()
    
        def expired(self):
            if self.count:
                if ( self.last_query_time + datetime.timedelta( milliseconds=self.period_ms ) ) > datetime.datetime.now():
                    return False
                else:
                    if self.count > 0:  self.count   = self.count-1
                    if self.count == 0: self.running = 0
                    self.last_query_time = datetime.datetime.now()
                    return True
            return False
    
    class App(object):
        def __init__(self):
            self.root = tk.Tk()
            self.label = tk.Label(text="")
            self.label.pack()
            self.timer = InteractiveTimer( period_ms=3*1000, count=-1 )
            self.timer.start()
            self.time = time.strftime("Hello World!!! %H:%M:%S")
            self.update_clock()
            self.root.mainloop()
            self.file2watch = "/home/smeckley/.hud/current_dir.txt"
    
        def update_clock(self):
            if self.timer.expired():
                self.time = time.strftime("Hello Strange World!!! %H:%M:%S")
            else:
                self.time = time.strftime("Hello World!!! %H:%M:%S")
            self.label.configure(text=self.time)
            self.root.after(1000, self.update_clock)
    
    
    app=App()
                                 

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
