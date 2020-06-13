---
title: lifx control
date: 2020-05-07
---
Example Python program lifx-control.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter
* import lifxlan

## Classes

* class Application(tkinter.Frame):

## Methods

* def sendCommand(self, type, val):
* def sendWithType(self, type):
* def f(val):
* def createWidgets(self):
* def __init__(self, master=None):

## Code

Python tkinter example

    import tkinter
    import lifxlan
    
    class Application(tkinter.Frame):
        def sendCommand(self, type, val):
            try:
                light = self.lights[int(self.selectedLight.get())]
            except ValueError:
                return
    
            if light is None:
                return
    
            if type not in ['hue', 'brightness', 'saturation', 'colortemp']:
                print("invalid type: %s" % type)
    
            func = getattr(light, 'set_' + type)
            func(val)
    
        def sendWithType(self, type):
            def f(val):
                return self.sendCommand(type, val)
            
            return f
    
        def createWidgets(self):
            self.lan = lifxlan.LifxLAN()
            self.lights = self.lan.get_color_lights()
    
            labelText = "\n".join([ "%d: %s" % (i, self.lights[i].get_label()) for i in range(len(self.lights)) ])
    
            label = tkinter.Label(self, text=labelText)
            label.pack()
    
            self.selectedLight = tkinter.StringVar(self)
            self.selectedLight.set("Select an option")
    
            self.lightSelector = apply(tkinter.OptionMenu, (self, self.selectedLight) + tuple(range(len(self.lights))))        
            self.lightSelector.pack()
    
            for type in ['hue', 'saturation', 'brightness', 'colortemp']:
                min = 2500 if type == 'colortemp' else 0
                max = 9000 if type == 'colortemp' else 2**16 - 1
    
                scale = tkinter.Scale(self, from_=min, to=max, 
                                      orient=tkinter.HORIZONTAL, 
                                      label=type, 
                                      command=self.sendWithType(type),
                                      length=200)
                scale.pack()
    
        def __init__(self, master=None):
            tkinter.Frame.__init__(self, master)
            self.pack()
            self.createWidgets()
    
    
    
    root = tkinter.Tk()
    app = Application(master=root)
    app.mainloop()
    root.destroy()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
