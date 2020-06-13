---
title: waydrn15
date: 2020-05-07
---
Example Python program waydrn15.py

## Modules

* import sys, os, Tkinter, time, random

## Methods

* def log_to_file(filename, formatted_time, entry, window):
* def ask_what_you_are_doing(mainwin, filename):
* def main(argv):

## Code

Python tkinter example

    #!/usr/bin/python
    # -*- coding: utf-8; -*-
    """Asks, "What are you doing right now?" at random, averaging every 15 minutes.
    
    Results are appended to `~/waydrn15.log` by default.
    
    """
    
    import sys, os, Tkinter, time, random
    
    def log_to_file(filename, formatted_time, entry, window):
        f = open(filename, 'a')
    
        try:
            f.write('%s %s\n' % (formatted_time, entry.get()))
        finally:
            f.close()
    
        window.destroy()
    
    def ask_what_you_are_doing(mainwin, filename):
        new_window = Tkinter.Toplevel()
    
        now = time.time()
        formatted_time = time.strftime('%H:%M', time.localtime(now))
        text = 'What are you doing right now? (%s)' % formatted_time
    
        label = Tkinter.Label(new_window, text=text)
        entry = Tkinter.Entry(new_window, width=80)
        datetime = time.strftime('%Y-%m-%d %H:%M', time.localtime(now))
        command = lambda: log_to_file(filename, datetime, entry, new_window)
        button = Tkinter.Button(new_window, text='Log it', command=command)
        button.bind('<Return>', lambda ev: button.invoke())
    
        for widget in [label, entry, button]:
            widget.pack()
    
        entry.focus()
        new_window.lift()      # raise above other windows, stealing focus
    
        seconds = random.expovariate(1.0/(15*60))
        # for debugging:
        # seconds = 5
        mainwin.after(int(1000 * seconds),
                      lambda: ask_what_you_are_doing(mainwin, filename))
    
    def main(argv):
        if len(argv) == 2:
            filename = argv[1]
        else:
            filename = os.path.join(os.environ['HOME'], 'waydrn15.log')
        
        mainwin = Tkinter.Tk()
        mainwin.title('time sampling applet')
        Tkinter.Label(mainwin,
                      text='Close this window to stop logging your time.').pack()
        Tkinter.Label(mainwin,
                      text='Logging to %r.' % filename).pack()
    
        ask_what_you_are_doing(mainwin, filename)
    
        mainwin.mainloop()
    
    if __name__ == '__main__':
        main(sys.argv)
    
    # Local Variables:
    # compile-command: "./waydrn15.py"
    # End:
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
