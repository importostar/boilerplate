---
title: countdown
date: 2020-05-07
---
Example Python program countdown.py

## Modules

* import sys
* import time
* import tkinter
* import ttk
* import tkinter
* import tkinter.ttk as ttk
* import Tkinter as tkinter
* import ttk
* import subprocess

## Classes

* class Countdown:

## Methods

* def __init__(self, root, delay, callback):
* def update(self, end_time):
* def cancel(self):

## Code

Python tkinter example

    import sys
    import time
    
    version = sys.hexversion
    if 0x03000000 <= version < 0x03010000 :
        import tkinter
        import ttk
    elif version >= 0x03010000:
        import tkinter
        import tkinter.ttk as ttk
    else: # version < 0x03000000
        import Tkinter as tkinter
        import ttk
    
    now = time.time #NOTE: subject to time adjustments
    
    class Countdown:
        "Show countdown and call `callback` in `delay` seconds unless cancelled."
        def __init__(self, root, delay, callback):
            self.frame = ttk.Frame(root, padding="5 5")
            self.frame.master = root #XXX
            self.callback = callback
            self.seconds_var = tkinter.StringVar()
            self.update_id = None
    
            ttk.Label(self.frame, textvariable=self.seconds_var).grid(row=1)
            ttk.Button(self.frame, text='Cancel', command=self.cancel).grid(row=2)
            self.frame.grid()
            self.frame.master.protocol("WM_DELETE_WINDOW", self.cancel)
            self.update(now() + delay)
    
        def update(self, end_time):
            """Update countdown or call the callback and exit."""
            if end_time <= now():
                self.callback()
                self.frame.master.destroy()
            else:
                self.seconds_var.set('%.0f' % (end_time - now()))
                self.update_id = self.frame.after(100, self.update, end_time)
    
        def cancel(self):
            """Cancel callback, exit."""
            if self.update_id is not None:
                self.frame.after_cancel(self.update_id)
            self.frame.master.destroy()
    
    if __name__=="__main__":
        import subprocess
    
        root = tkinter.Tk()
        Countdown(root, 10, lambda: subprocess.call(['pkill', 'gedit']))
        root.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
