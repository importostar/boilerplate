---
title: sync_gui
date: 2020-05-07
---
Example Python program sync_gui.py

## Modules

* import os
* import tkinter as tk
* from tkinter import filedialog
* from tkinter import ttk
* from tkinter import scrolledtext
* import time
* import threading

## Classes

* class DirectoryPicker(tk.Button):
* class App():

## Methods

* def __init__(self, root, *args, **kwargs):
* def openDirectory(self):
* def __init__(self, worker_function):
* def show(self):
* def run(self):
* def set_active(self, bool_val):
* def write(self, text):
* def setupWidgets(self):
* def worker(args):

## Code

Python tkinter example

    #!/usr/bin/env python3
    
    import os
    import tkinter as tk
    from tkinter import filedialog
    from tkinter import ttk
    from tkinter import scrolledtext
    import time
    import threading
    
    class DirectoryPicker(tk.Button):
        """
        Subclass of tkinter button.
        Button that shows folder selection dialog on click and selected folder path as text.
        """
        def __init__(self, root, *args, **kwargs):
            super().__init__(root, *args, **kwargs)
            self.directory = None
            self.root = root
            self.placeholder = 'Select a folder'
            self.configure(text=self.placeholder)
            self.configure(command=self.openDirectory)
    
        def openDirectory(self):
            home = os.path.expanduser('~')
            path = filedialog.askdirectory(parent=self.root, initialdir=home, title=self.placeholder)
            self["text"] = str(path) if path else self.placeholder
            self.directory = path
    
    class App():
        """
        GUI using tkinter. Shows main window with .show().
        Pass a function in the constructor to be executed when the start button is clicked.
        The function is passed a dictionary of the arguments set in the GUI elements.
        """
        def __init__(self, worker_function):
            self.root = tk.Tk()
            self.root.title('reSyncable')
            self.setupWidgets()
            self.worker_function = worker_function
    
        def show(self):
            # Place window in middle of screen
            self.root.eval('tk::PlaceWindow %s center' % self.root.winfo_pathname(self.root.winfo_id()))
            self.root.mainloop()
    
        def run(self):
            """
            Function that is called when the start button is clicked.
            Collects all the arguments to be passed to the worked function
            and runs it in a spearate thread, so the main UI remains responsive.
            """
            args = {
                'sync_dir': self.sync_dir_btn["text"],
                'another_dir': self.another_dir_btn['text'],
                'third_dir': self.third_dir_btn['text']
            }
            threading.Thread(target=self.worker_function, args=[args]).start()
    
        def set_active(self, bool_val):
            if bool_val:
                self.start_btn['state'] = 'disabled'
                self.progress.grid(column=0, row=6, columnspan=2, sticky=tk.W+tk.E)
                self.progress.start()
            else:
                self.start_btn['state'] = 'normal'
                self.progress.stop()
                self.progress.grid_forget()
    
        def write(self, text):
            """
            Write to the text area at the bottom of the GUI.
            """
            self.log.configure(state='normal')
            self.log.insert(tk.END, text + '\n')
            self.log.yview(tk.END) # Autoscroll to the bottom
            self.log.configure(state='disabled')
    
        def setupWidgets(self):
            # Folder selection dialog
            tk.Label(self.root, text="Sync directory").grid(row=0, sticky=tk.W)
            self.sync_dir_btn = DirectoryPicker(self.root, padx=10)
            self.sync_dir_btn.grid(row=0, column=1, padx=(10, 0), sticky=tk.W)
    
            tk.Label(self.root, text="Another directory").grid(row=1, sticky=tk.W)
            self.another_dir_btn = DirectoryPicker(self.root, padx=10)
            self.another_dir_btn.grid(row=1, column=1, padx=(10, 0), sticky=tk.W)
    
            tk.Label(self.root, text="A third directory").grid(row=2, sticky=tk.W)
            self.third_dir_btn = DirectoryPicker(self.root, padx=10)
            self.third_dir_btn.grid(row=2, column=1, padx=(10, 0), sticky=tk.W)
    
            self.start_btn = tk.Button(self.root, text="Start syncing", padx=20, command=self.run)
            self.start_btn.grid(column=0, row=4, columnspan=2, pady=10)
    
            self.log = scrolledtext.ScrolledText(self.root, width=40, height=10)
            self.log.configure(font='TkFixedFont')
            self.log.configure(state='disabled')
            self.log.grid(column=0, row=5, columnspan=2, sticky=tk.W+tk.E)
    
            self.progress = ttk.Progressbar(self.root, orient="horizontal", mode="indeterminate")
    
    
    if __name__ == "__main__":
    
        def worker(args):
            app.set_active(True)
            # this is where the actual work is being done
            app.write('Started syncing')
            app.write('Got args: {}'.format(args))
            for _ in range(3):
                # Report time / date at 1-second intervals
                app.write('Current time: ' + time.asctime())
                time.sleep(1)
            app.write('Done syncing')
            app.set_active(False)
    
        app = App(worker)
        app.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
