---
title: button_panel
date: 2020-05-07
---
Example Python program button_panel.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from __future__ import print_function
* from sys import stdin, stdout, argv
* import Tkinter
* import sh

## Methods

* def make_button(*args, **kwargs):
* def add_command(frame, name, cmd):
* def button():
* def make_panel(master, button_spec):
* def main():

## Code

Python tkinter example

    #!/usr/bin/env python
    
    from __future__ import print_function
    from sys import stdin, stdout, argv
    import Tkinter
    import sh
    
    # PUBLIC DOMAIN.
    #   - Lucretiel
    
    def make_button(*args, **kwargs):
        return lambda func: Tkinter.Button(*args, command=func, **kwargs)
    
    def add_command(frame, name, cmd):
        @make_button(frame, text=name)
        def button():
            try:
                proc = sh.sh(c=cmd, _out=stdout, _in=stdin)
            except sh.ErrorReturnCode as e:
                print("ERROR:", e)
        button.pack(side='top', fill='x', expand=True)
        print("Added button {name} for `{cmd}`".format(
            name=name, cmd=cmd))
    
    def make_panel(master, button_spec):
        frame = Tkinter.Frame(master)
        frame.pack(expand=True, fill='both', side='top')
        
        for line in button_spec:
            add_command(frame, *line.strip().split(None, 1))
    
        return frame
    
    def main():
        top = Tkinter.Tk()
        
        make_panel(top, stdin)
        
        top.mainloop()
    
    if __name__ == '__main__':
        main()
    
    #
    # Sample button spec:
    #
    #    Build make -j debug64
    #    Deploy cp debug64/bin/binary dest/binary
    #    Launch service restart binary
    #    Debug gdbserver 0.0.0.0:50000 $(get_pid binary)
    #

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
