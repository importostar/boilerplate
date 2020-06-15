---
title: GUIsTkinter
date: 2020-05-07
---
Example Python program GUIsTkinter.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import matplotlib
* from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg, NavigationToolbar2Tk
* from matplotlib.figure import Figure
* import matplotlib.animation as animation
* from matplotlib import style
* import tkinter as tk
* from tkinter import ttk
* import urllib
* import json
* import pandas as pd
* from pandas.io.json import json_normalize
* import numpy as np
* import sqlite3

## Classes

* class MainApp(tk.Tk):
* class StartPage(tk.Frame):
* class PageOne(tk.Frame):
* #class PageTwo(tk.Frame):
* class BTCPage(tk.Frame):

## Methods

* def animate(i):
* def __init__(self, *args, **kwargs):
* def show_frame(self, cont):
* def __init__(self, parent, controller):
* def __init__(self, parent, controller):
* #def __init__(self, parent, controller):
* def __init__(self, parent, controller):

## Code

Python tkinter example

    import matplotlib
    from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg, NavigationToolbar2Tk
    from matplotlib.figure import Figure
    import matplotlib.animation as animation
    from matplotlib import style
    import tkinter as tk
    from tkinter import ttk
    import urllib
    import json
    import pandas as pd
    from pandas.io.json import json_normalize
    import numpy as np
    import sqlite3
    
    matplotlib.use("TkAgg")
    
    LARGE_FONT = ("Verdana", 12)
    style.use("ggplot")
    
    f = Figure(figsize=(10, 6), dpi=100)
    a = f.add_subplot(111)
    
    
    def animate(i):
        dataLink = 'https://www.alphavantage.co/query?function=TIME_SERIES_INTRADAY&symbol=MSFT&interval=5min&outputsize=full&apikey=ZXI3K50Y8IV646HH'
        data = urllib.request.urlopen(dataLink)
        data = data.read().decode("utf-8")
        #data = json_normalize(data["Time Series (5min)"])
        data = json.loads(data)
        data = data["Time Series (5min)"]['2019-10-24 12:20:00']
        print(data)
        data = pd.DataFrame(data)
    
        date = []
    
        for k in data.keys():
            date.append(k)
        date.reverse()
        date = np.array(date, dtype="datetime64[s]")
        open = []
        high = []
        low = []
        close = []
    
        for k in data:
            open.append(data[k]["1. open"])
            high.append(data[k]["2. high"])
            low.append(data[k]["3. low"])
            close.append(data[k]["4. close"])
        open.reverse()
        high.reverse()
        low.reverse()
        close.reverse()
    
        open = np.array(open, dtype='float16')
        high = np.array(high, dtype='float64')
        low = np.array(low, dtype='float64')
        close = np.array(close, dtype='float64')
    
        a.clear()
        pd.plotting.register_matplotlib_converters()
        a.plot_date(date, high, "g", label="high")
        a.plot_date(date, low, "r", label="low")
        a.plot_date(date, open, "b", label="open")
        a.plot_date(date, close, "y", label="close")
    
        a.legend(bbox_to_anchor=(0, 1.02, 1, .102), loc=3, ncol=2, borderaxespad=0)
    
        title = "Wykres MSTF"
        a.set_title(title)
    
    
    class MainApp(tk.Tk):
    
        def __init__(self, *args, **kwargs):
            tk.Tk.__init__(self, *args, **kwargs)
    
            tk.Tk.iconbitmap(self, default="icon2.ico")
            tk.Tk.wm_title(self, "Program")
    
            container=tk.Frame(self)
            container.pack(side="top", fill="both", expand = True)
            container.grid_rowconfigure(0, weight=1)
            container.grid_columnconfigure(0, weight=1)
    
            self.frames = {}
    
            for F in (StartPage, BTCPage):
                frame = F(container, self)
                self.frames[F] = frame
                frame.grid(row=0, column=0, sticky="nsew")
    
            self.show_frame(StartPage)
    
        def show_frame(self, cont):
    
            frame = self.frames[cont]
            frame.tkraise()
    
    
    class StartPage(tk.Frame):
    
        def __init__(self, parent, controller):
            tk.Frame.__init__(self, parent)
            label = tk.Label(self, text="""ALPHA Bitcoin trading application
            use at your own risk. There is no promise
            of warranty.""", font=LARGE_FONT)
            label.pack(pady=10, padx=10)
    
            button1 = ttk.Button(self, text="Agree", command=lambda: controller.show_frame(BTCPage))
            button1.pack()
            button2 = ttk.Button(self, text="Disagree", command=quit)
            button2.pack()
    
    
    class PageOne(tk.Frame):
    
        def __init__(self, parent, controller):
            tk.Frame.__init__(self, parent)
            label = tk.Label(self, text="Page One!", font=LARGE_FONT)
            label.pack(pady=10, padx=10)
    
            button1 = ttk.Button(self, text="Back to Home", command=lambda: controller.show_frame(StartPage))
            button1.pack()
            #button2 = ttk.Button(self, text="Visit Page 2", command=lambda: controller.show_frame(PageTwo))
            #button2.pack()
    
    
    #class PageTwo(tk.Frame):
    
        #def __init__(self, parent, controller):
            #tk.Frame.__init__(self, parent)
            #label = tk.Label(self, text="Page Two!", font=LARGE_FONT)
            #label.pack(pady=10, padx=10)
    
            #button = ttk.Button(self, text="Visit Page 1", command=lambda: controller.show_frame(PageOne))
            #button.pack()
            #button2 = ttk.Button(self, text="Back to Home", command=lambda: controller.show_frame(StartPage))
            #button2.pack()
    
    
    class BTCPage(tk.Frame):
    
        def __init__(self, parent, controller):
            tk.Frame.__init__(self, parent)
            label = tk.Label(self, text="Graph Page!", font=LARGE_FONT)
            label.pack(pady=10, padx=10)
    
            button = ttk.Button(self, text="Back to Home", command=lambda: controller.show_frame(StartPage))
            button.pack()
    
            canvas = FigureCanvasTkAgg(f, self)
            canvas.draw()
            toolbar = NavigationToolbar2Tk(canvas, self)
            toolbar.update()
    
            canvas._tkcanvas.pack(side=tk.BOTTOM, fill=tk.BOTH, expand=True)
            canvas.get_tk_widget().pack(side=tk.TOP, fill=tk.BOTH, expand=True)
    
    
    app = MainApp()
    ani = animation.FuncAnimation(f, animate, interval=1000)
    app.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
