---
title: treeview_table
date: 2020-05-07
---
Example Python program treeview_table.py

## Modules

* from Tkinter import N, E, W, S, END, YES, BOTH
* from ttk import Frame, Treeview, Scrollbar
* import tkFont
* import logging
* from Tkinter import Tk

## Classes

* class TreeTable(Frame):

## Methods

* def __init__(self, master, headers, data, name=None):
* def sortby(self, col, descending):

## Code

Python tkinter example

    from Tkinter import N, E, W, S, END, YES, BOTH
    from ttk import Frame, Treeview, Scrollbar
    import tkFont
    import logging
    
    class TreeTable(Frame):
        """
        A table based on :class:`ttk.Treeview`.
    
        :Parameters:
            **master** : Tkinter or ttk widget
                The widget in which the :class:`TableTree` will reside.
            **headers** : list of str
                The column headers for the table.
            **data** : list of tuples
                Table data. There must be as many elements in each tuple as there \
                are headers. Each tuple in the list corresponds to a row in the \
                table.
        """
        def __init__(self, master, headers, data, name=None):
            Frame.__init__(self, master, name=name)
            #: column headers
            self.headers = headers
            #: table data
            self.data = data
            #: :class:`~ttk.Treeview` that only shows "headings" not "tree columns"
            self.tree = Treeview(self, columns=self.headers, show="headings",
                                 name='tabletree')
            #: vertical scrollbar
            self.yscroll = Scrollbar(self, orient="vertical",
                                     command=self.tree.yview, name='table_yscroll')
            #: horizontal scrollbar
            self.xscroll = Scrollbar(self, orient="horizontal",
                                     command=self.tree.xview, name='table_xscroll')
            self.tree['yscrollcommand'] = self.yscroll.set  # bind to scrollbars
            self.tree['xscrollcommand'] = self.xscroll.set
            # position widgets and set resize behavior
            self.tree.grid(column=0, row=0, sticky=(N + E + W + S))
            self.yscroll.grid(column=1, row=0, sticky=(N + S))
            self.xscroll.grid(column=0, row=1, sticky=(E + W))
            self.grid_columnconfigure(0, weight=1)
            self.grid_rowconfigure(0, weight=1)
            # build tree
            for col in self.headers:
                # NOTE: Use col as column identifiers, crafty!
                # NOTE: Also change col to title case using str.title()
                # NOTE: make lambda behave nicely in a loop using default arg!
                callback = lambda c=col: self.sortby(c, False)
                self.tree.heading(col, text=col.title(), command=callback)
                # adjust the column's width to the header string
                self.tree.column(col, width=tkFont.Font().measure(col.title()))
            # insert a new top-level treeview item by suing an empty string
            for item in self.data:
                self.tree.insert('', END, values=item)
                # adjust column's width if necessary to fit each value
                for idx, val in enumerate(item):
                    col_width = tkFont.Font().measure(val)
                    # option can be specified at least 3 ways: as (a) width=None,
                    # (b) option='width' or (c) 'width', where 'width' can be any
                    # valid column option.
                    if self.tree.column(self.headers[idx], 'width') < col_width:
                        self.tree.column(self.headers[idx], width=col_width)
    
        def sortby(self, col, descending):
            """
            Sort table contents when a column header is clicked.
    
            :Parameters:
                **col**
                    The column identifier of the column to sort.
                **descending**
                    False if ascending, True if descending, switches each time.
            """
            logging.debug('sortby %s, descending: %s', col, descending)
            # grab values to sort
            data = [(self.tree.set(child, col), child)
                    for child in self.tree.get_children('')]
            # now sort the data in place
            data.sort(reverse=descending)
            for idx, item in enumerate(data):
                self.tree.move(item[1], '', idx)
            # switch the heading so it will sort in the opposite direction
            callback = lambda: self.sortby(col, not descending)
            self.tree.heading(col, command=callback)
    
    
    if __name__ == "__main__":
        from Tkinter import Tk
        dummy_data = [('holy grail', 1975), ('meaning of life', 1983),
                       ('life of brian', 1979), ('jabberwocky', 1977),
                       ('time bandits', 1981), ('brazil', 1985),
                       ('12 monkeys', 1995),
                       ('adventures of baron von munchausen', 1988)]
        headers = ['movie title', 'year']
        root = Tk()
        treetable = TreeTable(root, headers=headers, data=dummy_data)
        treetable.tree['height'] = 4
        treetable.pack(expand=YES, fill=BOTH)
        treetable.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
