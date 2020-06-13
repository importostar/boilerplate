---
title: asker5
date: 2020-05-07
---
Example Python program asker5.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import argparse # https://docs.python.org/3.5/library/argparse.html
* import tkinter as tk# https://docs.python.org/3.5/library/tkinter.html
* import tkinter.ttk as ttk   # https://docs.python.org/3.5/library/tkinter.ttk.html
* import tables3 as tb# local

## Classes

* class Asker(ttk.Frame):

## Methods

* def __init__(self, root=None, center=False, verbosity=0):
* def _create_widgets(self):
* def new_results(self):
* def addline(self):
* def tattler(self, who):
* def match(self,entries):
* def _clear_entries(self, entries):

## Code

Python tkinter example

    #!/usr/bin/env python3
    """Find a matching record in the database
    
    Last Modified: Wed Dec 27 05:00:23 PST 2017
    """
    
    import argparse             # https://docs.python.org/3.5/library/argparse.html
    import tkinter as tk        # https://docs.python.org/3.5/library/tkinter.html
    import tkinter.ttk as ttk   # https://docs.python.org/3.5/library/tkinter.ttk.html
    import tables3 as tb        # local
    
    class Asker(ttk.Frame):
        def __init__(self, root=None, center=False, verbosity=0):
            super().__init__(root)
            self.root = root
            self.verbosity = verbosity
            root.title("Asker")
            self.pack()
            self.results_owner = None
            self.results_frame = None
            self.iteration = 0
            self._create_widgets()
            if center:
                center_window(root)
    
        _pairs = (
                ('Your ID', 'user_id'),
                ('Sheet #', 'sheet_id'),
                ('Last Name', 'name_last'),
                ('First Name', 'name_first'),
                ('Number', 'house_number'),
                ('Street','street'),
                ('City', 'city')
        )
    
        def _create_widgets(self):
            msgtx = "NOTE: Navigate with mouse or with TAB and Shift-TAB"
            tx1 = ttk.Label(root, width=len(msgtx), text=msgtx, anchor='w')
            tx1.pack(side=tk.TOP, fill=tk.X, padx=2, pady=2)
            self.entries = []
            for pair in self._pairs:
                field = pair[0]
                row = tk.Frame(root)
                lab = ttk.Label(row, width=10, text=field, anchor='w')
                ent = ttk.Entry(row, width=32)
                row.pack(side=tk.TOP, anchor='w', padx=2, pady=1)
                lab.pack(side=tk.LEFT)
                ent.pack(side=tk.RIGHT, expand=tk.YES, fill=tk.X)
                self.entries.append((field, ent))
            noterow2 = tk.Frame(root)
            msgtx = "NOTE: Use SPACE or mouse click on buttons"
            tx2 = ttk.Label(noterow2, width=len(msgtx), text=msgtx, anchor='w')
            noterow2.pack(side=tk.TOP, fill=tk.X, padx=2, pady=2)
            tx2.pack(side=tk.LEFT, padx=5, pady=2)
    
            buttonrow = tk.Frame(root)
            buttonrow.pack(side=tk.TOP, fill=tk.X, padx=2, pady=2)
            b1 = ttk.Button(buttonrow, text='Find', command=(lambda e=self.entries: self.match(e)))
            b1.pack(side=tk.LEFT, padx=5, pady=2)
    
            b2 = ttk.Button(buttonrow, text='Quit', command=root.quit)
            b2.pack(side=tk.LEFT, padx=5, pady=2)
    
            test1 = ttk.Button(buttonrow, text='Line+', command= self.addline)
            test1.pack(side=tk.LEFT, padx=5, pady=2)
                    
            test2 = ttk.Button(buttonrow, text='New Search', command=self.new_results)
            test2.pack(side=tk.LEFT, padx=5, pady=2)
    
            self.results=None
            self.new_results()
    
            self.root.update()
            self.root.geometry("%sx%s" % (1160, 740))
    
        def new_results(self):
            if isinstance(self.results, tb.Table):
                self.results.destroy()
            self.results = tb.Table(self.root, ["Choose", "Name" + str(self.iteration+1), "#", "Street", "City"],
                    padx=1, pady=1,
                    button_column=0, button_text="Click", button_command=self.tattler,
                    cell_anchor=tk.W,
                    header_anchor=tk.W,
                    column_minwidths=[6, 44, 10, 33, 20],
                    scroll_horizontally=True)
            self.results.pack(side=tk.TOP, fill=tk.X,  pady=2)
            self.iteration += 1
    
        def addline(self):
            self.results.insert_row(
                    ["Row "+str(self.iteration),
                        "name from the resulting record though it should never be as long as this excruciatingly prolix one is",
                        str(self.iteration),
                        "some street or avenue",
                        "city of residence"
                    ]
                )
    
            self.root.update()
            self.iteration += 1
    
        def tattler(self, who):
            print("And the winner is",who)
    
        def match(self,entries):
            criteria = 0
            compare = ''
            for index in range(len(entries)):
                crit = self._pairs[index][1]
                entry = entries[index]
                field = entry[0]
                text = entry[1].get()
                if text is not None and text != '':
                    criteria += 1
            if criteria == 0:
                print(" *** ERROR: no fields entered")
                return
            self._clear_entries(entries)
    
        def _clear_entries(self, entries):
            for index in range(len(entries)):
                entry = entries[index]
                entry[1].delete(0,tk.END)
    
    if __name__ == '__main__':
        parser = argparse.ArgumentParser(description="A program find a voter record to match a petition signature")
        parser.add_argument("--dbname", default=None,
                help="name of the database to work on (overrides qubic.ini file)")
        parser.add_argument("--center", "-c", action="store_true",
                help="center the window when starting up")
        parser.add_argument("--verbosity","--verbose","-v",action="count",default=0,
                help="increase output verbosity")
        args=parser.parse_args()
    
        root = tk.Tk()
        s=ttk.Style()
        s.configure('me.TButton',background='lawn green')  # https://wiki.tcl.tk/37701
        s.configure('name.TButton',background='peru')  # https://wiki.tcl.tk/37701
        s.configure('number.TButton',background='pink')  # https://wiki.tcl.tk/37701
        s.configure('street.TButton',background='PeachPuff')  # https://wiki.tcl.tk/37701
        s.configure('city.TButton',background='sky blue')  # https://wiki.tcl.tk/37701
        anti = Asker(root=root, center=args.center, verbosity=args.verbosity)
        anti.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
