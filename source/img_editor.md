---
title: img_editor
date: 2020-05-07
---
Example Python program img_editor.py

## Modules

* from tkinter import *
* from tkinter import messagebox
* from tkinter import filedialog
* from PIL import ImageGrab

## Methods

* def locate(event):
* def draw(event):
* def get_img(event):
* def maximize(event):
* def minimize(event):

## Code

Python tkinter example

    from tkinter import *
    from tkinter import messagebox
    from tkinter import filedialog
    from PIL import ImageGrab
    
    def locate(event):
    	global x
    	global y
    	x = event.x
    	y = event.y
    
    def draw(event):
    	canvas.create_line(x, y, event.x, event.y, fill="black", width=3)
    	locate(event)
    
    def get_img(event):
    	x1 = root.winfo_rootx() + widget.winfo_x()
    	y1 = root.winfo_rooty() + widget.winfo_y()
    	x2 = x + widget.winfo_width()
    	y2 = y + widget.winfo_height()
    	ImageGrab.grab().crop((x1,y1,x2,y2)).save("file.png") #Windows only
    
    def maximize(event):
    	root.attributes("-fullscreen", True)
    	root.bind("<F11>", minimize)
    
    def minimize(event):
    	root.attributes("-fullscreen", False)
    	root.bind("<F11>", maximize)
    
    root = Tk()
    root.geometry("600x480")
    menu = Menu(root)
    canvas = Canvas(root, cursor="cross")
    
    root.bind("<F11>", maximize)
    canvas.bind("<Motion>", locate)
    canvas.bind("<B1-Motion>", draw)
    root.bind("<Control-S>", get_img)
    
    if __name__ == '__main__':
    	canvas.pack(fill="both", expand=True)
    	root.config(menu=menu)
    	root.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
