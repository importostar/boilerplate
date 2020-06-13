---
title: pygest_4_1
date: 2020-05-07
---
Example Python program pygest_4_1.py


## Classes

* class View():

## Methods

* def __init__(self, root_object):
* def set_up(self):
* def configure_mainframe(self):
* def configure_outputs(self):

## Code

Python tkinter example

    class View():
        """
        The main view class for the PyGest tkinter interface.
        """
        def __init__(self, root_object):
            self.root = root_object
            self.mainframe = None
            self.filePath = None
            self.set_up()
    
        def set_up(self):
            """
            Run necessary view and widget configuration methods.
            """
            self.configure_root()
            self.configure_mainframe()
            self.configure_banner()
            self.configure_inputs()
            self.configure_outputs()
        .
        .
        .
        def configure_mainframe(self):
            """
            Configure the main frame in the root cell with grid geometry manager.
            """
            logging.info("We are in the configure_mainframe method")
            self.mainframe = tkinter.Frame(self.root, background='blue')
            self.mainframe.grid(column=0, row=0, sticky=('N', 'S', 'E', 'W'))
            self.mainframe.columnconfigure(0, weight=1)
            self.mainframe.rowconfigure(0, weight=0)
            self.mainframe.rowconfigure(1, weight=1)
            self.mainframe.rowconfigure(2, weight=1)
        .
        .
        .
        def configure_outputs(self):
            """
            Configure output widgets: hash value, match value.
            """
            logging.info("We're in the configure_outputs method")
            outputs_frame = tkinter.Frame(self.mainframe, background="green", borderwidth=2, relief='flat')
            outputs_frame.grid(row=2, column=0, sticky=('N', 'S', 'E', 'W'))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
