---
title: tkinter_add_ons
date: 2020-05-07
---
Example Python program tkinter_add_ons.py

## Modules

* import tkinter as tk
* import pandas as pd
* from tkinter import ttk
* import_data: Imports a pandas DataFrame or numpy Array into the DataGridView
* self.import_data(df, col_map)
* def import_data(self, df, col_map=None):
* import numpy as np
* testView.import_data(testPack, testColMap)

## Classes

* class Stdout_to_Widget(object):
* class Window(tk.Tk):
* class Popup(tk.Toplevel):
* class ScrolledFrame(tk.Frame):
* class DataGridView(ScrolledFrame):

## Methods

*   def __init__(self, widget, disable=False):
*   def write(self, text):
* def __init__(self, padding=4, bgColor='cadet blue', title='User Window', width=640, height=480,
* def set_padding(self, *args, padding=None):
* def row_config(self, widget, weights):
* def col_config(self, widget, weights):
* def grid_config(self, widget, row_weights, col_weights):
* def display(self):
* def __init__(self, master, padding=5, title='Popup', bgColor='cadet blue', width=240, height=240,
* def set_padding(self, *args, padding=None):
* def row_config(self, widget, weights):
* def col_config(self, widget, weights):
* def grid_config(self, widget, row_weights, col_weights):
* def __init__(self, window, *args, **kwargs):
* def _reconfigure(self, event=None):
* def grid(self, row, column, sticky='nsew', rowspan=1, columnspan=1, **kwargs):
* def test_pack(self):
* def _make_ref(*args):
* def _to_dataframe(df):
* def __init__(self, window, df=None, col_map=None, **kwargs):
* def _build_col_map(self, col_map):
* def _combo_resize(self, event):
* def _combo_configure(self, event):
* def import_data(self, df, col_map=None):
* def clear(self):
* def get_data(self):

## Code

Python tkinter example

    import tkinter as tk
    import pandas as pd
    
    from tkinter import ttk
    
    class Stdout_to_Widget(object):
      """Class to catch sys.stdout and display real-time to a tkinter Text or Listbox widget
      
      Attributes:
        widget (tkinter.Text/tkinter.Listbox): tkinter Text or Listbox to display stdout data
        disable (bool): Choose to disable the widget after writing text
        toplevel (tkinter.Tk/tkinter.Toplevel): Toplevel of widget; updates to give real-time text display
        
      Methods:
        write: Catches sys.stdout.write or print events, sends text to widget provided, and updates the window
      """
      
      def __init__(self, widget, disable=False):
        self.widget = widget
        self.disable = disable
        self.toplevel = widget.winfo_toplevel()
        
      def write(self, text):
        if self.widget.cget('state') == 'disabled':
          self.widget.configure(state='normal')
          
        self.widget.insert(tk.END, text)
        self.widget.see(tk.END)
        self.toplevel.update()
        
        if self.disable:
          self.widget.configure(state='disabled')
        
    
    class Window(tk.Tk):
        """Class to build a tkinter-based main window with default values; base class for multiple
        window-based user utilities
        
        Attributes:
            defaultPad (int): Default padding for frames and widgets
            defaultBG (str): Default background color for frames and widgets
            
        Methods:
            set_padding: Sets padx and/or pady padding for widget provided
            row_config: Configures rows using a provided dictionary 'weights'
            col_config: Configures columns using a provided dictionary 'weights'
            grid_config: Configures rows and columns using 'weights' dictionaries
            display: Displays the currently configured Window
        """
        
        def __init__(self, padding=4, bgColor='cadet blue', title='User Window', width=640, height=480,
                     resize_width=True, resize_height=True, font=('Arial',10,'bold')):
            super().__init__()
            self.defaultPad = padding
            self.defaultBG = bgColor
            self.font = font
            
            self.title(title)
            
            center_width = width // 2
            center_height = height // 2
            self.geometry('{}x{}+{}+{}'.format(width, height, 
                          self.winfo_screenwidth() // 2 - center_width,
                          self.winfo_screenheight() // 2 - center_height))
            
            self.resizable(width=resize_width, height=resize_height)
            self.configure(bg=self.defaultBG)
    
        def set_padding(self, *args, padding=None):
            """Sets the x/y padding for a widget or widgets
    
            Args:
                *args: A tkinter or ttk widget or widgets
                padding (int/tuple): Padding in pixels
            """
            if not padding:
                padding = self.defaultPad
            
            if isinstance(padding, tuple):
                for arg in args:
                    if 'ttk' in str(type(arg)):
                        arg['padding'] = padding
                    else:
                        arg['padx'] = padding[0]
                        arg['pady'] = padding[1]
            elif isinstance(padding, int):
                for arg in args:
                    if 'ttk' in str(type(arg)):
                        arg['padding'] = tuple([padding for i in range(4)])
                    else:
                        arg['padx'] = padding
                        arg['pady'] = padding
    
        def row_config(self, widget, weights):
            """Configures rows for selected widget
            
            Args:
                widget (tkinter[widget]): Widget to configure rows
                weights (dict): Dictionary of row indices and associated desired weights
            """
            for key in weights.keys():
                widget.rowconfigure(int(key), weight=weights[key])
    
        def col_config(self, widget, weights):
            """Identical to row_config(), but for column configuration
            """
            for key in weights.keys():
                widget.columnconfigure(int(key), weight=weights[key])
                
        def grid_config(self, widget, row_weights, col_weights):
            """Configures row and column weights
            
            Args:
                widget (tkinter[widget]): the widget to configure
                row_weights (dict): weights for the widget rows
                col_weights (dict): weights for the widget columns
            """
            self.row_config(widget, row_weights)
            self.col_config(widget, col_weights)
    
        def display(self):
            """Displays the Window object as currently configured
            """
            self.mainloop()
    
            
    class Popup(tk.Toplevel):
        """Class to build a tkinter-based popup window with default values; pretty much the same as
        Window class without creating a new instance of tkinter.Tk
        
        Attributes:
            defaultPad (int): Default padding for frames and widgets
            defaultBG (str): Default background color for frames and widgets
            
        Methods:
            set_padding: Sets padx and/or pady padding for widget provided
            row_config: Configures rows using a provided dictionary 'weights'
            col_config: Configures columns using a provided dictionary 'weights'
            grid_config: Configures rows and columns using 'weights' dictionaries
        """
        
        def __init__(self, master, padding=5, title='Popup', bgColor='cadet blue', width=240, height=240,
                     font=('Arial',10,'bold'), resize_width=False, resize_height=False, **kwargs):
            super().__init__(master=master, **kwargs)
            
            self.defaultPad = padding
            self.defaultBG = bgColor
            self.font = font
            
            self.title(title)
            
            center_width = width // 2
            center_height = height // 2
            self.geometry('{}x{}+{}+{}'.format(width, height, 
                          self.winfo_screenwidth() // 2 - center_width,
                          self.winfo_screenheight() // 2 - center_height))
            
            self.resizable(width=resize_width, height=resize_height)
            self.configure(bg=self.defaultBG)
    
        def set_padding(self, *args, padding=None):
            """Sets the x/y padding for a widget or widgets
    
            Args:
                *args: A tkinter or ttk widget or widgets
                padding (int/tuple): Padding in pixels
            """
            if not padding:
                padding = self.defaultPad
            
            if isinstance(padding, tuple):
                for arg in args:
                    if 'ttk' in str(type(arg)):
                        arg['padding'] = padding
                    else:
                        arg['padx'] = padding[0]
                        arg['pady'] = padding[1]
            elif isinstance(padding, int):
                for arg in args:
                    if 'ttk' in str(type(arg)):
                        arg['padding'] = tuple([padding for i in range(4)])
                    else:
                        arg['padx'] = padding
                        arg['pady'] = padding
    
        def row_config(self, widget, weights):
            """Configures rows for selected widget
            
            Args:
                widget (tkinter[widget]): Widget to configure rows
                weights (dict): Dictionary of row indices and associated desired weights
            """
            for key in weights.keys():
                widget.rowconfigure(int(key), weight=weights[key])
    
        def col_config(self, widget, weights):
            """Identical to row_config(), but for column configuration
            """
            for key in weights.keys():
                widget.columnconfigure(int(key), weight=weights[key])
                
        def grid_config(self, widget, row_weights, col_weights):
            """Configures row and column weights
            
            Args:
                widget (tkinter[widget]): the widget to configure
                row_weights (dict): weights for the widget rows
                col_weights (dict): weights for the widget columns
            """
            self.row_config(widget, row_weights)
            self.col_config(widget, col_weights)
    
            
    class ScrolledFrame(tk.Frame):
        """SubClass of tkinter.Frame - contains a canvas and attached Frame linked to
        vertical and horizontal scrollbars.
    
        Methods:
            grid: Sets the ScrolledFrame in parent window, arranges canvas and scrollbars within Frame
            test_pack: For testing/debugging; generates 20 labels from top-left to bottom-right
        """
        
        def __init__(self, window, *args, **kwargs):
            super().__init__(window, *args, **kwargs)
    
            self.rowconfigure(0, weight=1)
            self.columnconfigure(0, weight=1)
    
            self._scrollbar_y = tk.Scrollbar(self)
            self._scrollbar_x = tk.Scrollbar(self, orient=tk.HORIZONTAL)
            
            self._canvas = tk.Canvas(self, borderwidth=0,
                                     xscrollcommand=self._scrollbar_x.set,
                                     yscrollcommand=self._scrollbar_y.set, **kwargs)
            self.frame = tk.Frame(self._canvas, **kwargs)
            self._window = self._canvas.create_window((0,0), window=self.frame, anchor='nw')
            
            self._scrollbar_x.configure(command=self._canvas.xview)
            self._scrollbar_y.configure(command=self._canvas.yview)
            
            self._canvas.bind('<Configure>', self._reconfigure)
            
        def _reconfigure(self, event=None):
            """Binds to Canvas <Configure> event, ensures canvas size fits the Frame and 
            the scrollbars have the right scrollregion
            """
            self.winfo_toplevel().update()
            bbox = self.frame.bbox('all')
            
            self._canvas.height = bbox[3]
            self._canvas.width = bbox[2]
            
            self._canvas.configure(scrollregion=bbox)
            
        def grid(self, row, column, sticky='nsew', rowspan=1, columnspan=1, **kwargs):
            """Sets ScrolledFrame in parent window; arranges canvas and scrollbars in Frame
    
            Args:
                ***Same as tkinter widget.grid() args
            """
            super().grid(row=row, column=column, sticky=sticky, rowspan=rowspan, columnspan=columnspan, **kwargs)
            self._spacer = tk.Frame(self)
            self._scrollbar_y.grid(row=0, column=1, sticky='ns')
            self._scrollbar_x.grid(row=1, column=0, sticky='ew')
            self._spacer.grid(row=1, column=1, sticky='nsew')
            self._canvas.grid(row=0, column=0, sticky='nsew')
            
        def test_pack(self):
            """Creates 20 raised Labels to test display/functionality
            """
            for i in range(20):
                widg = tk.Label(self.frame, text='Label {}'.format(str(i)), relief='raised')
                widg.grid(row=i, column=i, sticky='nsew')
            
            
    class DataGridView(ScrolledFrame):
        """Allows display of data in user interactive form using
        a variety of widget types.
    
        Methods:
            import_data: Imports a pandas DataFrame or numpy Array into the DataGridView
            clear: Destroys all widgets currently in the DataGridView
            get_data: Exports the current data from the DataGridView to a pandas DataFrame
        """
        
        @staticmethod
        def _make_ref(*args):
            return ','.join(args)
        
        @staticmethod
        def _to_dataframe(df):
            """Attempts to convert input 'df' to a pandas DataFrame
            """
            if not isinstance(df, (pd.DataFrame, type(None))):
                df = pd.DataFrame(df, columns=[str(x) for x in range(df.shape[1])])
                return df
            elif df is None:
                return pd.DataFrame()
            else:
                return df
        
        def __init__(self, window, df=None, col_map=None, **kwargs):
            super().__init__(window, **kwargs)
            
            self._datavars = {}
            self.import_data(df, col_map)
        
        def _build_col_map(self, col_map):
            """Builds a mapping dictionary which will direct the type of widget
            to use for each column of data.  Defaults to tkinter.Entry() if not found
            or not specified.
    
            Args:
                col_map (dict): Dictionary of column names and widget types.  Combobox types
                                require the values list to be included.
                                Example: {'ID' : 'Checkbox', 'Type' : ['Combobox', list(type_values)]}
    
            Returns:
                return_map (dict): Mapping dictionary of final column names and corrected widget types.
            """
            if col_map is None:
                return_map = {str(col) : 'Entry' for col in self._datagrid.columns}
            else:
                col_map = {str(x):y for x, y in col_map.items()}
                return_map = {str(col) : col_map.get(col, 'Entry') for col in self._datagrid.columns}
                
            return return_map
        
        def _combo_resize(self, event):
            """Resizes combobox width based on selection; bound to the <<ComboboxSelected>> event.
            """
            combo = event.widget
            testWidth = len(str(combo.get()))
            
            if testWidth > combo.cget('width'):
                combo.config(width=testWidth)
            else:
                return
            
        def _combo_configure(self, event):
            """Resizes the popdown menu to the longest option in the menu or to the required width of the Combobox,
            whichever is shorter; bound to the <ButtonPress> event.
            """
            combo = event.widget
            style = ttk.Style()
            
            long = max(combo.cget('values'), key=len)
    
            font = tkfont.nametofont(str(combo.cget('font')))
            width = max(0, font.measure(long.strip() + '0') - combo.winfo_width())
            
            style.configure('TCombobox', postoffset=(0,0,width,0))
        
        def import_data(self, df, col_map=None):
            """Imports data from df, builds grid of widgets, types determined by col_map dictionary
    
            Args:
                df (pandas.DataFrame OR numpy.array): Data to display in the DataGridView
                col_map (dict): ***See col_map description in _build_col_map***
            """
            self._datagrid = self._to_dataframe(df).fillna(value='')
            
            self._col_map = self._build_col_map(col_map)
            self._col_index = {self._datagrid.columns.get_loc(x) : x for x in self._datagrid.columns}
            
            self.clear()
            
            for col in self._datagrid.columns:
                if isinstance(self._col_map[col], list):
                    col_type = self._col_map[col][0]
                else:
                    col_type = self._col_map[col]
                    
                header = tk.Label(self.frame, text=col, relief='raised')
                header.grid(row=0, column=self._datagrid.columns.get_loc(col), sticky='nsew')
                
                for row in range(self._datagrid.shape[0]):
                    ref = self._make_ref(str(row), str(self._datagrid.columns.get_loc(col)))
                    val = self._datagrid.at[row, col]
                    
                    if col_type == 'Label':
                        self._datavars[ref] = tk.StringVar()
                        cell = tk.Label(self.frame, text=val, relief='raised', textvariable=self._datavars[ref])
                    elif col_type == 'Combobox':
                        self._datavars[ref] = tk.StringVar()
                        cell = ttk.Combobox(self.frame, state='readonly', values=self._col_map[col][1],
                                            textvariable=self._datavars[ref])
                        cell.bind('<<ComboboxSelected>>', self._combo_resize)
                        cell.bind('<ButtonPress>', self._combo_configure)
                    elif col_type == 'Checkbox':
                        self._datavars[ref] = tk.IntVar()
                        cell = tk.Checkbutton(self.frame, variable=self._datavars[ref], relief='raised')
                    else:
                        self._datavars[ref] = tk.StringVar()
                        cell = tk.Entry(self.frame, textvariable=self._datavars[ref], relief='raised')
                        cell.insert(0, str(self._datagrid.at[row,col]))
                    
                    self._datavars[ref].set(val if val is not None else '')
                    cell.grid(row=row + 1, column=self._datagrid.columns.get_loc(col), sticky='nsew')
                    width = len(str(val))
                    
                    if width > cell.cget('width'):
                        cell.config(width=width + 1)
                        
            self._reconfigure()
        
        def clear(self):
            for widget in self.frame.winfo_children():
                widget.destroy()
        
        def get_data(self):
            packupList = list(([self._datavars[x].get() for x in self._datavars.keys() if x.split(',')[0] == str(y)]
                                for y in range(self._datagrid.shape[0])))
            return pd.DataFrame(packupList, columns=self._datagrid.columns)
    
    
    if __name__ == '__main__':
        """Demo tkinter window containing one DataGridView and three other widgets
        in the same parent widget.
        """
    
        import numpy as np
        
        testFrame = tk.Tk()
        testPack = np.zeros((20,10))
        testColMap = {1:'Label', 2:['Combobox', [1,2,3,4,5]], 3:'Checkbox'}
        
        for i in range(2):
            testFrame.rowconfigure(i, weight=100)
            testFrame.columnconfigure(i, weight=100)
        
        testView = DataGridView(testFrame)
        testView.import_data(testPack, testColMap)
        testView.grid(row=0, column=0, sticky='nsew')
    
        lblOne = tk.Label(testFrame, text='Test1', relief='raised')
        lblOne.grid(row=1, column=0, sticky='nsew')
        lblTwo = tk.Label(testFrame, text='Test2', relief='raised')
        lblTwo.grid(row=0, column=1, sticky='nsew')
        lblThree = tk.Label(testFrame, text='Test3', relief='raised')
        lblThree.grid(row=1, column=1, sticky='nsew')
    
        testFrame.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
