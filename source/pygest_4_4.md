---
title: pygest_4_4
date: 2020-05-07
---
Example Python program pygest_4_4.py


## Classes

* class View():

## Methods

* def configure_outputs(self):

## Code

Python tkinter example

    class View():
        """
        The main view class for the PyGest tkinter interface.
        """
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
            outputs_frame.rowconfigure(0, weight=1)
            outputs_frame.rowconfigure(1, weight=1)
            outputs_frame.columnconfigure(0, weight=1)
            outputs_frame.columnconfigure(1, weight=1)
    
            hash_value_label = tkinter.Label(outputs_frame, text="Hash Value:")
            hash_value_label.grid(row=0, column=0, sticky='E')
    
            self.hash_value = tkinter.StringVar()
            self.hash_value.set("Default Hash Value Text")
    
            self.hash_value_entry = tkinter.Entry(outputs_frame, state='readonly', readonlybackground='white', fg='black')
            self.hash_value_entry.config(textvariable=self.hash_value, relief='flat', highlightthickness=0)
            self.hash_value_entry.grid(row=0, column=1, sticky=('W'))
    
            result_label = tkinter.Label(outputs_frame, text="Result:")
            result_label.grid(row=1, column=0, sticky='E')
    
            self.result_var = tkinter.StringVar()
            self.result_var.set("Default Result Text")
    
            result_display_label = tkinter.Label(outputs_frame, textvariable=self.result_var)
            result_display_label.grid(row=1, column=1, sticky=('W'))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
