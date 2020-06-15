---
title: waydrn15 (1)
date: 2020-05-07
---
Example Python program waydrn15 (1).py

## Modules

* import sys, os, Tkinter, time, random
* # and configure Tk widgets (unless you import a zillion names into

## Classes

* class TkinterWrapper:

## Methods

* def __init__(self, underlying_widget):
* def __getattr__(self, name):
* def _attach_subwidget_method(name):
* def subwidget_method(self, *args, **kwargs):
* def Tk(*args, **kwargs):
* def Toplevel(*args, **kwargs):
* def pack(*args, **kwargs):
* def append_to_file(filename, astring):
* def log_to_file(filename, formatted_time, entry, window):
* def ask_what_you_are_doing(mainwin, filename):
* def schedule_question(mainwin, filename):
* def main(argv):

## Code

Python tkinter example

    #!/usr/bin/python
    # -*- coding: utf-8; -*-
    """Asks, "What are you doing right now?" at random, averaging every 15 minutes.
    
    Results are appended to `~/waydrn15.log` by default.
    
    """
    
    import sys, os, Tkinter, time, random
    
    
    ### Tkinter interface
    
    # This is because Tkinter makes it unnecessarily difficult to create
    # and configure Tk widgets (unless you import a zillion names into
    # your own namespace).
    
    class TkinterWrapper:
        "Simple wrapper to make it easier to create Tk subwidgets."
    
        def __init__(self, underlying_widget):
            self.underlying_widget = underlying_widget
    
        def __getattr__(self, name):
            return getattr(self.underlying_widget, name)
    
    def _attach_subwidget_method(name):
        widget_class = getattr(Tkinter, name)
        def subwidget_method(self, *args, **kwargs):
            return widget_class(self.underlying_widget, *args, **kwargs)
        setattr(TkinterWrapper, name, subwidget_method)
    
    for widget_class_name in 'Label Entry Button'.split():
        _attach_subwidget_method(widget_class_name)
    
    
    def Tk(*args, **kwargs):
        return TkinterWrapper(Tkinter.Tk(*args, **kwargs))
    def Toplevel(*args, **kwargs):
        return TkinterWrapper(Tkinter.Toplevel(*args, **kwargs))
    
    def pack(*args, **kwargs):
        for widget in args:
            widget.pack(**kwargs)
    
    
    ### Application code
    
    def append_to_file(filename, astring):
        f = open(filename, 'a')
    
        try:
            f.write(astring)
        finally:
            f.close()
        
    
    def log_to_file(filename, formatted_time, entry, window):
        message = entry.get().encode('utf-8')
        append_to_file(filename, '%s %s\n' % (formatted_time, message))
        window.destroy()
    
    def ask_what_you_are_doing(mainwin, filename):
        new_window = Toplevel()
    
        entry = new_window.Entry(width=80)
    
        now = time.localtime(time.time())
        datetime = time.strftime('%Y-%m-%d %H:%M', now)
        command = lambda: log_to_file(filename, datetime, entry, new_window)
        button = new_window.Button(text='Log it', command=command)
        button.bind('<Return>', lambda ev: button.invoke())
    
        text = 'What are you doing right now? (%s)' % time.strftime('%H:%M', now)
        pack(new_window.Label(text=text), entry, button)
    
        entry.focus()
        new_window.lift()      # raise above other windows, stealing focus
    
        schedule_question(mainwin, filename)
    
    def schedule_question(mainwin, filename):
        seconds = random.expovariate(1.0/(15*60))
        # for debugging: seconds = 5
        mainwin.after(int(1000 * seconds),
                      lambda: ask_what_you_are_doing(mainwin, filename))
    
    def main(argv):
        if len(argv) == 2:
            filename = argv[1]
        else:
            filename = os.path.join(os.environ['HOME'], 'waydrn15.log')
        
        mainwin = Tk()
        mainwin.title('time sampling applet')
        pack(mainwin.Label(text='Close this window to stop logging your time.'),
             mainwin.Label(text='Logging to %r.' % filename))
    
        schedule_question(mainwin, filename)
    
        mainwin.mainloop()
    
    if __name__ == '__main__':
        main(sys.argv)
    
    # Local Variables:
    # compile-command: "./waydrn15.py"
    # End:
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
