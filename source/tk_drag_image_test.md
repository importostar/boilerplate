---
title: tk_drag_image_test
date: 2020-05-07
---
Example Python program tk_drag_image_test.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PIL import Image
* from tkinter import *
* from tkinter import Tk, BOTH
* from tkinter.ttk import Frame, Label, Style

## Classes

* class LabelImage(Frame):
* class Example(Frame):

## Methods

* def __init__(self, parent, name, x, y):
* def on_mouse_down(self, event):
* def on_drag(self, event):
* def __init__(self):
* def add_image(self, name, x, y):
* def initUI(self):
* def main():

## Code

Python tkinter example

    #!/usr/bin/python3
    # -*- coding: utf-8 -*-
    
    from PIL import Image
    from tkinter import *
    from tkinter import Tk, BOTH
    from tkinter.ttk import Frame, Label, Style
    
    class LabelImage(Frame):
        def __init__(self, parent, name, x, y):
            super().__init__(parent, border=4)   
            photo = PhotoImage(file=name)
            photo_label = Label(parent, image=photo)         
            photo_label.image = photo
            photo_label.place(x=x, y=y)
            self.img = photo_label
            self.x = x
            self.y = y
            self.ox = self.oy = 0
            
            photo_label.bind("<Button-1>", self.on_mouse_down)
            photo_label.bind("<B1-Motion>", self.on_drag)
        
        def on_mouse_down(self, event):
            self.ox = event.x 
            self.oy = event.y 
            
        def on_drag(self, event):
            x = event.x 
            y = event.y 
            #print(x, y)
            dx = (x - self.ox) 
            dy = (y - self.oy) 
            self.x += dx
            self.y += dy        
            self.img.place(x=self.x, y=self.y)
    
                    
    class Example(Frame):
      
        def __init__(self):
            super().__init__()            
            self.initUI()
            
        def add_image(self, name, x, y):
            photo = PhotoImage(file=name)
            photo_label = Label(image=photo)         
            photo_label.image = photo
            photo_label.place(x=x, y=y)
            
        def initUI(self):
            self.canvas = Canvas(self.master, bg="#000000")
            self.master.title("Absolute positioning")
            self.pack(fill=BOTH, expand=1)
            
            Style().configure("TFrame", background="#333")
            self.img1 = LabelImage(self, "test/example.png", 20, 20)
            self.img2 = LabelImage(self, "test/test.png", 40, 260)
            self.img3 = LabelImage(self, "test/fire.png", 340, 300)
    
            
    def main():
      
        root = Tk()
        root.geometry("640x480+300+300")
        app = Example()
        root.mainloop()  
    
    
    if __name__ == '__main__':
        main()  
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
