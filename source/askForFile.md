---
title: askForFile
date: 2020-05-07
---
Example Python program askForFile.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from tkinter import filedialog
* from tkinter import Tk
* from pathlib import Path
* from typing import List, Set, Dict, Tuple, Optional

## Methods

* def ask_for_file(
* def ask_for_directory(msg: str = "Please, choose a directory.") -> Optional[Path]:

## Code

Python tkinter example

    #!/usr/bin/env python3
    # -*- coding=utf-8 -*-
    """
    Code snippet for prompting a familiar tkinter GUI to ask user to select 
    a specific file or directory in their computer.
    No dependencies needed.
    
    Tested with Python 3.7
    G.Berthiaume 2019
    """
    from tkinter import filedialog
    from tkinter import Tk
    from pathlib import Path
    from typing import List, Set, Dict, Tuple, Optional
    
    
    def ask_for_file(
        valid_file_types: List, strict: bool = False, msg: str = "Please, choose a file."
    ) -> Optional[Path]:
        """Ask user to select a file with a gui.
    
        Args:
            valid_file_types:   List of tupple that represent valid file types. 
                                e.g. [("image", "*.jpeg"), ("text", "*.txt")] 
            strict:             If true, it wont give user the option to choose "all files". 
            msg:                The message at the top of the window.
        
        Returns:
            pathlib.Path object if user has selected a file
            None if user has cancel the prompt
        """
        if not strict:
            valid_file_types.append(("All files", "*.*"))
    
        # We don't want a full GUI, so keep the root window from appearing
        Tk().withdraw()
    
        # Show dialog box and return the path to the selected file
        filepath = filedialog.askopenfilename(
            initialdir=Path.cwd(), filetypes=(valid_file_types), title=msg
        )
    
        if filepath == "":
            # user as pressed "cancel" or as quitted
            return None
    
        return Path(filepath)
    
    
    def ask_for_directory(msg: str = "Please, choose a directory.") -> Optional[Path]:
        """Ask user to select a directory with a gui.
    
        Args:
            msg: The message at the top of the window.
        
        Returns:
            pathlib.Path object if user has selected a directory
            None if user has cancel the prompt
        """
        # We don't want a full GUI, so keep the root window from appearing
        Tk().withdraw()
    
        # Show dialog box and return the path to the selected file
        dirpath = filedialog.askdirectory(title=msg)
    
        if dirpath == "":
            # user as pressed "cancel" or as quitted
            return None
    
        return Path(dirpath)
    
    
    if __name__ == "__main__":
        # Example 1
        valid_file_types = [("Great text !", "*.txt"), ("Nice image !", "*.jpeg")]
        filepath = ask_for_file(valid_file_types, strict=True)
    
        if filepath is not None:
            print(filepath)
            print(f"> This file" + " does exist." if filepath.exists() else "does not exist.")
    
        # Example 2
        dirpath = ask_for_directory()
        if dirpath is not None:
            print(dirpath)
            print(f"> This directory" + " does exist." if dirpath.exists() else "does not exist.")
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
