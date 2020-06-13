---
title: c
date: 2020-05-07
---
Example Python program c.py

## Modules

* import tkinter
* import random
* import _thread

## Classes

* class Menu:

## Methods

* def __init__(self):
* def get_serial_data(self):

## Code

Python tkinter example

    import tkinter
    import random
    import _thread
    
    
    class Menu:
        def __init__(self):
            self.window = tkinter.Tk()
    
            # define a frame to hold values
            self.updatable_display = tkinter.Frame(self.window)
    
            # define an initial weight placeholder and label
            self.weight_value = tkinter.StringVar()
            self.weight_label = tkinter.Label(self.updatable_display,
                                              textvariable=self.weight_value
                                              )
            # Pack it for window sizing
            self.updatable_display.pack()
            self.weight_label.pack()
    
            # After window loads, use a thread to update window with new data from get_serial_data
            self.window.after(0, _thread.start_new_thread, self.get_serial_data, ())
    
            tkinter.mainloop()
    
        def get_serial_data(self):
            # update the previously defined weight value
            while True:
                self.weight_value.set(str(random.randrange(133777, 439932)))
                # add a sensible sleep for a half second maybe?
    
    
    # Call it
    gui = Menu()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
