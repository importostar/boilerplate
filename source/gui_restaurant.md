---
title: gui_restaurant
date: 2020-05-07
---
Example Python program gui_restaurant.py

## Modules

* import Tkinter

## Methods

* def submit():

## Code

Python tkinter example

    import Tkinter
    
    #global variables
    dish_v = None
    price_v = None
    
    def submit():
    	print dish_v
    	print price_v
    	dailymenu_file=open("dailymenu.txt", "w")
    	dailymenu_file.write("Daily menu:\n")
    	dailymenu_file.write(dish_v)
    	dailymenu_file.write(price_v)
    	dailymenu_file.close()
    
    # main window
    window = Tkinter.Tk()
    window.title("Daily Menu:")
    
    # main container
    frame = Tkinter.Frame(window)
    
    # lay out the main container, specify that we want it to grow with window size
    frame.pack(fill=Tkinter.BOTH, expand=True)
    
    #create widgets
    label_dish = Tkinter.Label(frame, text="new dish:")
    dish = Tkinter.Entry(frame, textvariable=dish_v)
    
    label_price = Tkinter.Label(frame, text="price:")
    price = Tkinter.Entry(frame, textvariable=price_v)
    
    button_submit = Tkinter.Button(frame, text="Submit", command=submit)
    
    # lay out widgets
    label_dish.grid(row=0, column=1, padx=5, pady=5)
    dish.grid(row=0, column=2, padx=5, pady=5)
    
    label_price.grid(row=1, column=1, padx=5, pady=5)
    price.grid(row=1, column=2, padx=5, pady=5)
    
    button_submit.grid(row=2, column=1, columnspan=2, padx=5, pady=5)
    
    # Run forever!
    window.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
