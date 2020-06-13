---
title: pygest_5_4
date: 2020-05-07
---
Example Python program pygest_5_4.py


## Classes

* class View():

## Methods

* def configure_buttons(self):
* def runHash(self):
* def clear(self):
* def processDigest(path, hash_type):

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
    
        def clear(self):
            """
            Clears all input and output fields.
            """
            logging.info("Clear button pressed.")
    
    def processDigest(path, hash_type):
        """
        Run hash function of type hash_type on file at path. Return digest.
        """
        if hash_type == "md5":
            hashFunc = hashlib.md5()
        else:
            hashFunc = hashlib.sha1()
    
        blockSize = 65535
        try:
            with open(path, 'rb') as target:
                buf = target.read(blockSize)
                while len(buf) > 0:
                    hashFunc.update(buf)
                    buf = target.read(blockSize)
            digested = hashFunc.hexdigest()
            return digested
        except (IOError, TypeError) as error:
            logging.debug("Error in hash func: {}".format(error))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
