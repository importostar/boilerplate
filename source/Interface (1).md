---
title: Interface (1)
date: 2020-05-07
---
Example Python program Interface (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter
* import numpy
* import guidata
* import thinkdsp
* import thinkplot
* import sys
* import matplotlib.patches as mpatches
* import matplotlib.lines as mlines
* import matplotlib.pyplot as pyplot
* import guidata.dataset.datatypes as dt
* import guidata.dataset.dataitems as di
* from guidata.qt.QtGui import (QPushButton, QApplication, QMessageBox, )
* from PyQt5.QtCore import Qt
* from PyQt5.QtWidgets import QWidget
* from matplotlib.backends.backend_tkagg import (FigureCanvasTkAgg, NavigationToolbar2TkAgg)
* from matplotlib.figure import Figure
* from tkinter import messagebox
* from IPython import get_ipython

## Classes

* class Start(dt.ActivableDataSet):

## Methods

* def callback(dataset, item, value, parent):
* def Signal(freq, amp, func):
* def Plot(signal, color, label, root, ax, fig):
* #def on_closing():

## Code

Example Python PyQt program :

    import tkinter
    import numpy
    import guidata
    import thinkdsp
    import thinkplot
    import sys
    
    import matplotlib.patches as mpatches
    import matplotlib.lines as mlines
    import matplotlib.pyplot as pyplot
    
    import guidata.dataset.datatypes as dt
    import guidata.dataset.dataitems as di
    from guidata.qt.QtGui import (QPushButton, QApplication, QMessageBox, )
    from PyQt5.QtCore import Qt
    from PyQt5.QtWidgets import QWidget
    
    from matplotlib.backends.backend_tkagg import (FigureCanvasTkAgg, NavigationToolbar2TkAgg)
    from matplotlib.figure import Figure
    from tkinter import messagebox
    
    from IPython import get_ipython
    #get_ipython().run_line_magic('matplotlib', 'inline')
    
    _app = guidata.qapplication()
    
    def callback(dataset, item, value, parent):
        root = tkinter.Tk()
        fig = pyplot.figure(figsize=(8, 4), dpi = 100)
        ax = fig.add_subplot(111)
        line_cos = mlines.Line2D([], [], color = dataset.cos_color, label = 'Cosseno')
        line_sin = mlines.Line2D([], [], color = dataset.sin_color, label = 'Seno')
        line_sinc = mlines.Line2D([], [], color = dataset.sinc_color, label = 'Seno Cardinal')
        line_tan = mlines.Line2D([], [], color = dataset.tan_color, label = 'Tangente')
        if dataset.cos_on:
            arg = 'CosSignal'
            sig = Signal(dataset.cos_freq, dataset.cos_amp, arg)
            ax.plot(sig.ts, sig.ys, color = dataset.cos_color, label = 'Cosseno')
            ax.set_xlabel('Frequência(Hz)')
            ax.set_ylabel('Amplitude')
            ax.legend(loc = 'upper right')
    #        Plot(sig, color = dataset.cos_color, label = 'Cosseno', root = root, ax = ax, fig = fig)
        if dataset.sin_on:
            arg = 'SinSignal'
            sig = Signal(dataset.sin_freq, dataset.sin_amp, arg)
            ax.plot(sig.ts, sig.ys, color = dataset.sin_color, label = 'Seno')
            ax.set_xlabel('Frequência(Hz)')
            ax.set_ylabel('Amplitude')
            ax.legend(loc = 'upper right')
    #        Plot(sig, color = dataset.sin_color, label = 'Seno', root = root, ax = ax, fig = fig)
        if dataset.sinc_on:
            arg = 'Sinc'
            sig = Signal(dataset.sinc_freq, dataset.sinc_amp, arg)
            ax.plot(sig.ts, sig.ys, color = dataset.sinc_color, label = 'Seno Cardinal')
            ax.set_xlabel('Frequência(Hz)')
            ax.set_ylabel('Amplitude')
            ax.legend(loc = 'upper right')
    #        Plot(sig, color = dataset.sinc_color, label = 'Seno Cardinal', root = root, ax = ax, fig = fig)
        if dataset.tan_on:
            arg = 'TanSignal'
            sig = Signal(dataset.sinc_freq, dataset.sinc_amp, arg)
            ax.plot(sig.ts, sig.ys, color = dataset.tan_color, label = 'Tangente')
            ax.set_xlabel('Frequência(Hz)')
            ax.set_ylabel('Amplitude')
            ax.legend(loc = 'upper right')
    #        Plot(sig, color = dataset.tan_color, label = 'Tangente', root = root, ax = ax, fig = fig)
    #    ax.legend([line_cos, line_sin, line_sinc, line_tan], ['Cosseno', 'Seno', 'Seno Cardinal', 'Tangente'])
            ax.legend(loc = 'upper right')
        
        Plot(sig, color = dataset.sinc_color, label = 'Seno Cardinal', root = root, ax = ax, fig = fig)
        
        tkinter.mainloop()
            
    def Signal(freq, amp, func):
        sig = eval('thinkdsp.{}({}, {}, offset = 0)'.format(func, freq, amp))
        period = (1.0 / sig.freq) * 2
        sig = sig.make_wave(period)
        return sig
    
    def Plot(signal, color, label, root, ax, fig):
        print("Aqui")
    #    signal.plot(color = color, label = label)
    #    thinkplot.config(xlabel = 'Frequência',
    #                     ylabel = 'Amplitude',
    #                     legend = True,
    #                     loc = 'upper right'
    #                     )
        #root = tkinter.Tk()
        #root.wm_title("Embedding in Tk")    
        canvas = FigureCanvasTkAgg(fig, master=root)  # A tk.DrawingArea.
        canvas.draw()
        canvas.get_tk_widget().pack(side=tkinter.TOP, fill=tkinter.BOTH, expand=1)
        
        toolbar = NavigationToolbar2TkAgg(canvas, root)
        toolbar.update()
        canvas._tkcanvas.pack(side=tkinter.TOP, fill=tkinter.BOTH, expand=1)
        
    #    def on_closing():
    #        #if messagebox.askokcancel("Quit", "Do you want to quit?"):
    #            root.destroy()
    #    
    #    root.protocol("WM_DELETE_WINDOW", on_closing)
    #    tkinter.mainloop()
    
    class Start(dt.ActivableDataSet):
        """Processamento de Sinais Digitais"""
        t_group = dt.BeginTabGroup("T group")
        
        cos = dt.BeginGroup("Cosseno")
        cos_on = di.BoolItem("Cosseno", default = False)
        cos_freq = di.FloatItem("Frequência (Hz)", default = 110)
        cos_amp = di.FloatItem("Amplitude", default = 1.0)
        cos_color = di.ColorItem("Color", default = "red")
        _cos = dt.EndGroup("Cosseno")
        
        sin = dt.BeginGroup("Seno")
        sin_on = di.BoolItem("Seno", default = False)
        sin_freq = di.FloatItem("Frequência (Hz)", default = 110)
        sin_amp = di.FloatItem("Amplitude", default = 1.0)
        sin_color = di.ColorItem("Color", default = "blue")
        _sin = dt.EndGroup("Seno")
        
        sinc = dt.BeginGroup("Seno Cardial")
        sinc_on = di.BoolItem("Seno Cardial", default = False)
        sinc_freq = di.FloatItem("Frequência (Hz)", default = 110)
        sinc_amp = di.FloatItem("Amplitude", default = 1.0)
        sinc_color = di.ColorItem("Color", default = "green")
        _sinc = dt.EndGroup("Seno Cardial")
        
        tan = dt.BeginGroup("Tangente")
        tan_on = di.BoolItem("Tangente", default = False)
        tan_freq = di.FloatItem("Frequência (Hz)", default = 110)
        tan_amp = di.FloatItem("Amplitude", default = 1.0)
        tan_color = di.ColorItem("Color", default = "yellow")
        _tan = dt.EndGroup("Tangente")
        
        _t_group = dt.EndTabGroup("T group")
    
        
        #type = di.ChoiceItem("Tipos de Gráficos",
        #                     ("Cosseno", "Seno", "Seno Cardial"))
        buttonOne = di.ButtonItem("Plotar Gráfico", callback)
    
    if __name__ == "__main__":
        # Create QApplication
        param = Start()
        arg = param.edit()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
