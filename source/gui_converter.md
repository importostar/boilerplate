---
title: gui_converter
date: 2020-05-07
---
Example Python program gui_converter.py

## Modules

* import Tkinter

## Methods

* def convert():

## Code

Python tkinter example

    import Tkinter
    
    # global variables
    temp_c = None
    temp_f = None
    
    def convert():
    
        global temp_c
        global temp_f
    
        try:
            val = temp_c.get()
            temp_f.set((val * 9.0 / 5) + 32)
        except:
            pass
    
    # main window
    window = Tkinter.Tk()
    window.title("Temperature Converter")
    
    # main container
    frame = Tkinter.Frame(window)
    
    # lay out the main container, specify that we want it to grow with window size
    frame.pack(fill=Tkinter.BOTH, expand=True)
    
    # allow middle cell of grid to grow when window is resized
    frame.columnconfigure(1, weight=1)
    frame.rowconfigure(1, weight=1)
    
    # variables for holding temperature data
    temp_c = Tkinter.DoubleVar()
    temp_f = Tkinter.DoubleVar()
    
    # create widgets
    entry_celsius = Tkinter.Entry(frame, width=7, textvariable=temp_c)
    label_unitc = Tkinter.Label(frame, text="degrees C")
    label_equal = Tkinter.Label(frame, text="is equal to")
    label_fahrenheit = Tkinter.Label(frame, textvariable=temp_f)
    label_unitf = Tkinter.Label(frame, text="degrees F")
    button_convert = Tkinter.Button(frame, text="Convert", command=convert)
    
    # lay out widgets
    entry_celsius.grid(row=0, column=1, padx=5, pady=5)
    label_unitc.grid(row=0, column=2, padx=5, pady=5, sticky=Tkinter.W)
    label_equal.grid(row=1, column=0, padx=5, pady=5, sticky=Tkinter.E)
    label_fahrenheit.grid(row=1, column=1, padx=5, pady=5)
    label_unitf.grid(row=1, column=2, padx=5, pady=5, sticky=Tkinter.W)
    button_convert.grid(row=2, column=1, columnspan=2, padx=5, pady=5, sticky=Tkinter.E)
    
    # Place cursor in entry box by default
    entry_celsius.focus()
    
    # Run forever!
    window.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
