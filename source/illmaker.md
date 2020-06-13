---
title: illmaker
date: 2020-05-07
---
Example Python program illmaker.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os
* from tkinter import *
* from tkinter.ttk import *
* from tkinter.colorchooser import *

## Classes

* class CustomButton(Canvas):
* class VerticalScrolledFrame(Frame):

## Methods

* def __init__(self, parent, width, height, color, command=None, retu=0, gyo=0, chaco=None):
* def _change_color(self, event):
* def _on_press(self, event):
* def _on_release(self, event):
* def __init__(self, parent, *args, **kw):
* def _configure_interior(event):
* def _configure_canvas(event):
* def file_input():
* def file_output(booltable):
* def off_light(buttontable, y, x):
* def on_light(buttontable, y , x):
* def on_off(buttontable, booltable,y,x):
* def change_color(lists, row):
* def add_light_amount(mylist, lists, buttontable, booltable, gyo=-1):
* def destroy_light_amount(lists, buttontable, booltable):

## Code

Python tkinter example

    #!/usr/bin/env python3
    import os
    from tkinter import *
    from tkinter.ttk import *
    from tkinter.colorchooser import *
    
    
    class CustomButton(Canvas):
        def __init__(self, parent, width, height, color, command=None, retu=0, gyo=0, chaco=None):
            Canvas.__init__(self, parent, borderwidth=1, relief="flat", highlightthickness=0)
            self.width = width
            self.height = height
            self.command = command
            self.retu = retu
            self.color = color
            self.chaco = chaco
    
            self.padding = padding = 4
    
            id = self.create_oval((padding, padding, width+padding, height+padding), outline=color, fill=color)
            (x0,y0,x1,y1)  = self.bbox("all")
            width = (x1-x0) + padding
            height = (y1-y0) + padding
            self.configure(width=width, height=height)
            self.bind("<ButtonPress-3>", self._change_color)
            self.bind("<ButtonPress-1>", self._on_press)
            self.bind("<ButtonRelease-1>", self._on_release)
    
        def _change_color(self, event):
            self.configure(relief="sunken")
            if self.chaco is not None:
                self.chaco()
            self.configure(relief="flat")
    
        def _on_press(self, event):
            self.configure(relief="sunken")
            if self.command is not None:
                self.command()
    
        def _on_release(self, event):
            self.configure(relief="flat")
    
    
    class VerticalScrolledFrame(Frame):
        def __init__(self, parent, *args, **kw):
            Frame.__init__(self, parent, *args, **kw)
    
            vscrollbar = Scrollbar(self, orient=VERTICAL)
            vscrollbar.pack(fill=Y, side=RIGHT, expand=FALSE)
            canvas = Canvas(self, bd=0, highlightthickness=0, yscrollcommand=vscrollbar.set)
            canvas.pack(side=LEFT, fill=BOTH, expand=TRUE)
            vscrollbar.config(command=canvas.yview)
    
            canvas.xview_moveto(0)
            canvas.yview_moveto(0)
    
            self.interior = interior = Frame(canvas)
            interior_id = canvas.create_window(0, 0, window=interior,
                                               anchor=NW)
    
            def _configure_interior(event):
                size = (interior.winfo_reqwidth(), interior.winfo_reqheight())
                canvas.config(scrollregion="0 0 %s %s" % size)
                if interior.winfo_reqwidth() != canvas.winfo_width():
                    canvas.config(width=interior.winfo_reqwidth())
                if interior.winfo_reqheight() != canvas.winfo_height():
                    canvas.config(height=interior.winfo_reqheight())
    
            interior.bind('<Configure>', _configure_interior)
    
            def _configure_canvas(event):
                if interior.winfo_reqwidth() != canvas.winfo_width():
                    canvas.itemconfigure(interior_id, width=canvas.winfo_width())
            canvas.bind('<Configure>', _configure_canvas)
    
    
    def file_input():
        if not os.path.exists('/home/pi/pythonProgram/dev/ptrdata.txt'):
            zero = "00000000"
            with open ('/home/pi/pythonProgram/dev/ptrdata.txt', 'w', encoding='utf8') as input:
    
                input.write(zero)
                for i in range(9):
                    c = '\n' + zero
                    input.write(c)
    
        with open ('/home/pi/pythonProgram/dev/ptrdata.txt', 'r', encoding='utf8') as input:
            strs = input.readlines()
            strs = list(map(lambda s: s.replace('\n',''), strs))
            strlen = len(strs)
            booltable = []
            for s in strs:
                lists = []
                for c in s:
                    if c == '0':
                        lists.append(False)
                    else:
                        lists.append(True)
                booltable.append(lists)
            return booltable
    
    def file_output(booltable):
        with open ('/home/pi/pythonProgram/dev/ptrdata.txt', 'w', encoding='utf8') as input:
            b0 =  booltable[0]
            for b in b0:
                input.write('1' if b else '0')
            for bools in booltable[1:]:
                input.write('\n')
                for b in bools:
                    input.write('1' if b else '0')
    
    def off_light(buttontable, y, x):
        color = buttontable[x][y].color
        color = int(color.replace('#',''), 16) // 2
        color = hex(color)
        color = color.replace("0x","#")
        buttontable[x][y].create_oval((buttontable[x][y].padding, buttontable[x][y].padding, buttontable[x][y].width+buttontable[x][y].padding, buttontable[x][y].height+buttontable[x][y].padding), outline='#000000', fill='#000000')
    
    def on_light(buttontable, y , x):
        buttontable[x][y].create_oval((buttontable[x][y].padding, buttontable[x][y].padding, buttontable[x][y].width+buttontable[x][y].padding, buttontable[x][y].height+buttontable[x][y].padding), outline=buttontable[x][y].color, fill=buttontable[x][y].color)
    
    def on_off(buttontable, booltable,y,x):
        booltable[x][y] = not booltable[x][y]
        if not booltable[x][y]:
            off_light(buttontable, y, x)
    
        else:
            on_light(buttontable, y, x)
    
        file_output(booltable)
    
    def change_color(lists, row):
        try :
            colors = askcolor()
            (a, b) = colors
            if a==None and b==None:
                return
            for item in lists:
                item[row].color = b
                item[row].create_oval((item[row].padding, item[row].padding, item[row].width+item[row].padding, item[row].height+item[row].padding), outline=b, fill=b)
    
            for gyo in range(len(booltable)):
                for retu in range(8):
                    if not booltable[gyo][retu]:
                        off_light(buttontable, retu, gyo)
        except _tkinter.TclError:
            pass
    
    def add_light_amount(mylist, lists, buttontable, booltable, gyo=-1):
        if gyo == -1:
            gyo = len(lists)
            var = []
            for i in range(8):
                var.append(False)
            booltable.append(var)
        frame = Frame(mylist.interior)
        buttons = []
        for retu in range(8):
            cb = CustomButton(frame, 100, 100, '#FF8C00', (lambda but=buttontable,bot=booltable,x=retu,y=gyo: on_off(but,bot,x,y)), retu, gyo, (lambda l=buttontable, r=retu: change_color(l,r)))
            buttons.append(cb)
            cb.pack(side = 'left', padx = 10)
        buttontable.append(buttons)
        lists.append(frame)
        lists[-1].pack()
        for retu in range(8):
            if not booltable[gyo][retu]:
                off_light(buttontable, retu, gyo)
        file_output(booltable)
    
    def destroy_light_amount(lists, buttontable, booltable):
        lists[-1].destroy()
        lists.pop()
        buttontable.pop()
        booltable.pop()
        file_output(booltable)
    
    if __name__ == '__main__':
        root = Tk()
        w, h = root.winfo_screenwidth(), root.winfo_screenheight()
        root.geometry("%dx%d+0+0" % (w, h))
        root.bind("<Escape>", lambda e: root.quit())
        root.title('Illmaker')
    
        lists = []
        buttontable = []
        booltable = file_input()
        print(len(booltable))
    
        top = Frame(root)
        light_pulse_button = Button(top,text='+',command=(lambda: add_light_amount(mylist, lists, buttontable, booltable)))
        light_pulse_button.pack(side = 'left')
        light_minus_button = Button(top,text='-',command=(lambda: destroy_light_amount(lists, buttontable, booltable)))
        light_minus_button.pack(side = 'left')
        top.pack()
    
    
        mylist = VerticalScrolledFrame(root, height=h)
        mylist.pack(fill = BOTH)
    
        for gyo in range(len(booltable)):
            add_light_amount(mylist, lists, buttontable, booltable, gyo)
    
        root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
