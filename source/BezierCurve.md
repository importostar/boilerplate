---
title: BezierCurve
date: 2020-05-07
---
Example Python program BezierCurve.py

## Modules

* import math
* import tkinter as tk
* from tkinter import ttk
* from tkinter import Scale
* from tkinter import HORIZONTAL
* import numpy as np

## Classes

* class BezierCurveApp(tk.Tk):
* class StartPage(tk.Frame):

## Methods

* def __init__(self, height = 800, width = 800, *args, **kwargs):
* def show_frame(self, cont):
* def __init__(self, parent, controller, height, width):
* def get_param(self,val):
* def show_point(self, event):
* def make_curve(self, event):
* def draw_lines(self,arr):
* def draw_lines_2(self,arr):
* def lerp(self,point1,point2,t_param):

## Code

Python tkinter example

    import math
    import tkinter as tk
    from tkinter import ttk
    from tkinter import Scale
    from tkinter import HORIZONTAL
    import numpy as np
    LARGE_FONT = ("Verdana", 12)
    
    class BezierCurveApp(tk.Tk):
    
        def __init__(self, height = 800, width = 800, *args, **kwargs):
    
            tk.Tk.__init__(self, *args, **kwargs)
            container = tk.Frame(self)
            container.pack(side="top", fill="both", expand=True)
    
            container.grid_rowconfigure(0, weight = 1)
            container.grid_columnconfigure(0, weight = 1)
            self.frames = {}
            frame = StartPage(container, self, height, width)
            self.frames[StartPage] = frame
            frame.grid(row=0, column = 0, sticky="nsew")
    
            self.show_frame(StartPage)
    
        def show_frame(self, cont):
    
            frame = self.frames[cont]
            frame.tkraise() 
    
    class StartPage(tk.Frame):
    
        def __init__(self, parent, controller, height, width):
            tk.Frame.__init__(self, parent)
            self.height = height
            self.width = width
            self.clicks = []
            self.param_point_ovals = []
            self.param_points = []
            self.lines = []
    
            self.param_points_2 = []
            self.param_point_ovals_2 = []
            self.lines_2 = []
            self.val = 0
            scale = Scale(self, from_=0, length=600, to=1, resolution = 0.01, orient=HORIZONTAL, command=self.get_param)
            scale.pack()
    
            label = tk.Label(self, text="Bezier Curve", font=LARGE_FONT)
            label.pack(pady =10,padx=10)
            self.canvas = tk.Canvas(height=self.height, width=self.width, bg='white')
            self.canvas.pack(fill=tk.BOTH, expand=True)
            self.left_click_bind = self.canvas.bind("<Button-1>", self.show_point)
            self.right_click_bind = self.canvas.bind("<Button-3>", self.make_curve)
      
        def get_param(self,val):
    
            self.val = val
            for point in self.param_point_ovals:
                self.canvas.delete(point)
    
            temp_param_point_ovals = []
            temp_param_points = [] 
            for _ in range(len(self.clicks)-1): 
                center = self.lerp((self.clicks[_][0],self.clicks[_][1]),(self.clicks[_+1][0],self.clicks[_+1][1]), float(val))
                temp_param_points.append(center)
                temp_param_point_ovals.append(self.canvas.create_oval(center[0]-2,center[1]-2,center[0]+2,center[1]+2, fill="green"))
            self.param_points = temp_param_points
            self.param_point_ovals = temp_param_point_ovals
            self.draw_lines(self.param_points)
    
            ##############
            if(len(self.clicks) == 4):
                for point in self.param_point_ovals_2:
                    self.canvas.delete(point)
    
            temp_param_point_ovals_2 = []
            temp_param_points_2 = [] 
            for _ in range(len(self.param_points)-1): 
                center = self.lerp((self.param_points[_][0],self.param_points[_][1]),(self.param_points[_+1][0],self.param_points[_+1][1]), float(val))
                temp_param_points_2.append(center)
                temp_param_point_ovals_2.append(self.canvas.create_oval(center[0]-2,center[1]-2,center[0]+2,center[1]+2, fill="green"))
            self.param_points_2 = temp_param_points_2
            self.param_point_ovals_2 = temp_param_point_ovals_2
            self.draw_lines_2(self.param_points_2)
    
            for _ in range(len(self.param_points_2)-1): 
                center = self.lerp((self.param_points_2[_][0],self.param_points_2[_][1]),(self.param_points_2[_+1][0],self.param_points_2[_+1][1]), float(val))
                self.canvas.create_oval(center[0]-2,center[1]-2,center[0]+2,center[1]+2, fill="yellow")        
    
        def show_point(self, event):
            self.clicks.append((event.x - 1, event.y - 1))
            self.canvas.create_oval(event.x-2, event.y-2, event.x+2, event.y+2, fill="red")
    
    
        def make_curve(self, event):
            self.canvas.unbind("<Button-1", self.left_click_bind)
            self.canvas.unbind("<Button-3", self.right_click_bind)
            # self.clicks.sort()
           
            for _ in range(len(self.clicks)-1):
                self.canvas.create_line(self.clicks[_][0],self.clicks[_][1],self.clicks[_+1][0],self.clicks[_+1][1], fill = "blue")  
                
                center = self.lerp((self.clicks[_][0],self.clicks[_][1]),(self.clicks[_+1][0],self.clicks[_+1][1]), 0)
                self.param_points.append(center)
                self.param_point_ovals.append(self.canvas.create_oval(center[0]-2,center[1]-2,center[0]+2,center[1]+2, fill="green"))
    
        def draw_lines(self,arr):
    
            for line in self.lines:
                self.canvas.delete(line)
    
            temp_lines = []    
            for _ in range(len(arr)-1):
                temp_lines.append(self.canvas.create_line(arr[_][0],arr[_][1],arr[_+1][0],arr[_+1][1], fill = "black"))
    
            self.lines = temp_lines
    
        def draw_lines_2(self,arr):
    
                for line in self.lines_2:
                    self.canvas.delete(line)
    
                temp_lines = []    
                for _ in range(len(arr)-1):
                    temp_lines.append(self.canvas.create_line(arr[_][0],arr[_][1],arr[_+1][0],arr[_+1][1], fill = "black"))
    
                self.lines_2 = temp_lines
    
           
        def lerp(self,point1,point2,t_param):
            return((point1[0]*(1-t_param)+point2[0]*t_param),(point1[1]*(1-t_param)+point2[1]*t_param))
    
    app = BezierCurveApp(height= 800, width = 800)
    app.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
