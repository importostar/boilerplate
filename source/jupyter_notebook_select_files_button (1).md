---
title: jupyter_notebook_select_files_button (1)
date: 2020-05-07
---
Example Python program jupyter_notebook_select_files_button (1).py

## Modules

* import traitlets
* from IPython.display import display
* from ipywidgets import widgets
* from tkinter import Tk, filedialog

## Classes

* class SelectFilesButton(widgets.Button):

## Methods

* def __init__(self, *args, **kwargs):
* def select_files(b):

## Code

Python tkinter example

    import traitlets
    from IPython.display import display
    from ipywidgets import widgets
    from tkinter import Tk, filedialog
    
    
    class SelectFilesButton(widgets.Button):
        """A file widget that leverages tkinter.filedialog."""
    
        def __init__(self, *args, **kwargs):
            """Initialize the SelectFilesButton class."""
            super(SelectFilesButton, self).__init__(*args, **kwargs)
            # Add the selected_files trait
            self.add_traits(files=traitlets.traitlets.List())
            # Create the button.
            self.description = "Select Files"
            self.icon = "square-o"
            self.style.button_color = "orange"
            # Set on click behavior.
            self.on_click(self.select_files)
    
        @staticmethod
        def select_files(b):
            """Generate instance of tkinter.filedialog.
    
            Parameters
            ----------
            b : obj:
                An instance of ipywidgets.widgets.Button
            """
            # Create Tk root
            root = Tk()
            # Hide the main window
            root.withdraw()
            # Raise the root to the top of all windows.
            root.call('wm', 'attributes', '.', '-topmost', True)
            # List of selected fileswill be set to b.value
            b.files = filedialog.askopenfilename(multiple=True)
    
            b.description = "Files Selected"
            b.icon = "check-square-o"
            b.style.button_color = "lightgreen"

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
