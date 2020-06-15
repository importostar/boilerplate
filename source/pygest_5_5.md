---
title: pygest_5_5
date: 2020-05-07
---
Example Python program pygest_5_5.py


## Classes

* class View():

## Methods

* def configure_buttons(self):
* def runHash(self):

## Code

Python tkinter example

    class View():
        """
        The main view class for the PyGest tkinter interface.
        """
        .
        .
        .
        def configure_buttons(self):
            """
            Configure button frame and two buttons: hash and clear.
            """
            logging.info("We're in the configure buttons method.")
            buttons_frame = tkinter.Frame(self.mainframe, background="blue", borderwidth=2, relief='flat')
            buttons_frame.grid(row=3, column=0,  sticky=('N', 'S', 'E', 'W'))
            buttons_frame.columnconfigure(0, weight=1)
            buttons_frame.rowconfigure(0, weight=1)
            buttons_frame.rowconfigure(1, weight=1)
    
            hash_button = tkinter.Button(buttons_frame, text='Hash', relief='raised', command=self.runHash)
            hash_button.grid(row=0, column=0, sticky=('N', 'S', 'E', 'W'))
    
            clear_button = tkinter.Button(buttons_frame, text='Clear', relief='raised', command=self.clear)
            clear_button.grid(row=1, column=0, sticky=('N', 'S', 'E', 'W'))
    
        def runHash(self):
            """
            Contains functionality to run the hash function.
            """
            logging.info("Hash button pressed.")
            path = self.filePath
            hash_func = self.radio_var.get()
            logging.info("File path: {}".format(path))
            logging.info("Hash func: {}".format(hash_func))
            digest = processDigest(path, hash_func)
            logging.info("Hash digest: {}".format(digest))
    
            self.hash_value.set(digest)
            new_hash_value_entry = self.hash_value_entry.get()
            logging.info("New Hash Value Entry: {}".format(new_hash_value_entry))
    
            user_input_digest_value = self.digest_entry.get()
    
            if user_input_digest_value == "":
                self.result_var.set("Done")
            elif user_input_digest_value == digest:
                self.result_var.set("Success! Digest match.")
            else:
                self.result_var.set("Fail! No match.")

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
