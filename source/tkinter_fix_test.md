---
title: tkinter_fix_test
date: 2020-05-07
---
Example Python program tkinter_fix_test.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from __future__ import absolute_import, division, print_function
* import os
* import sys
* import platform
* These modules will be automatic imported by tkinter import.
* and import the fix module.
* If the fix module was imported before, then we reload it.
* import FixTk
* from tkinter import _fix
* from imp import reload
* import tkinter as tk
* import Tkinter as tk

## Methods

* def fix_virtualenv_tkinter():
* def get_python_info():

## Code

Python tkinter example

    
    from __future__ import absolute_import, division, print_function
    
    import os
    import sys
    import platform
    
    
    def fix_virtualenv_tkinter():
        """
        work-a-round for tkinter under windows in a virtualenv:
          "TclError: Can't find a usable init.tcl..."
        Known bug, see: https://github.com/pypa/virtualenv/issues/93
    
        There are "fix tk" file here:
    
              C:\Python27\Lib\lib-tk\FixTk.py
              C:\Python34\Lib\tkinter\_fix.py
    
        These modules will be automatic imported by tkinter import.
    
        The fix set theses environment variables:
    
            TCL_LIBRARY C:\Python27\tcl\tcl8.5
            TIX_LIBRARY C:\Python27\tcl\tix8.4.3
            TK_LIBRARY C:\Python27\tcl\tk8.5
    
            TCL_LIBRARY C:\Python34\tcl\tcl8.6
            TIX_LIBRARY C:\Python34\tcl\tix8.4.3
            TK_LIBRARY C:\Python34\tcl\tk8.6
    
        but only if:
    
              os.path.exists(os.path.join(sys.prefix,"tcl"))
    
        And the virtualenv activate script will change the sys.prefix
        to the current env. So we temporary change it back to sys.real_prefix
        and import the fix module.
        If the fix module was imported before, then we reload it.
        """
        if "TCL_LIBRARY" in os.environ:
            # Fix not needed (e.g. virtualenv issues #93 fixed?)
            return
    
        if not hasattr(sys, "real_prefix"):
            # we are not in a activated virtualenv
            return
    
        if sys.version_info[0] == 2:
            # Python v2
            virtualprefix = sys.prefix
            sys.prefix = sys.real_prefix
    
            import FixTk
    
            if "TCL_LIBRARY" not in os.environ:
                reload(FixTk)
    
            sys.prefix = virtualprefix
        else:
            # Python v3
            virtualprefix = sys.base_prefix
            sys.base_prefix = sys.real_prefix
    
            from tkinter import _fix
    
            if "TCL_LIBRARY" not in os.environ:
                from imp import reload
                reload(_fix)
    
            sys.base_prefix = virtualprefix
    
    
    def get_python_info():
        implementation = platform.python_implementation()
        if implementation == "CPython":
            return "%s v%s [%s]" % (
                implementation,
                platform.python_version(),
                platform.python_compiler(),
            )
            # e.g.: CPython v2.7.6 [GCC 4.8.2]
        elif implementation == "PyPy":
            ver_info = sys.version.split("(", 1)[0]
            ver_info += sys.version.split("\n")[-1]
            return "Python %s" % ver_info
            # e.g.: Python 2.7.6 [PyPy 2.3.1 with GCC 4.8.2]
        else:
            return "%s %s" % (
                sys.executable,
                sys.version.replace("\n", " ")
            )
    
    
    if __name__ == "__main__":
        print("sys.platform.....:", sys.platform)
        print("Python info......:", get_python_info())
        print("sys.prefix.......:", sys.prefix)
        print("sys.real_prefix..:", getattr(sys, "real_prefix", "<not in a virtualenv>"))
    
        print()
    
        if sys.platform.startswith("win"):
            print(" * Apply Tk fix.")
            fix_virtualenv_tkinter()
        else:
            print(" * No Windows -> no fix needed.")
    
        if sys.version_info[0] == 3:
            import tkinter as tk
        else:
            import Tkinter as tk
    
        print()
    
        print("TCL_LIBRARY..:", os.environ.get("TCL_LIBRARY", "<not set>"))
        print("TIX_LIBRARY..:", os.environ.get("TIX_LIBRARY", "<not set>"))
        print("TK_LIBRARY...:", os.environ.get("TK_LIBRARY", "<not set>"))
    
        print()
    
        print("Tkinter patchlevel:", tk.Tcl().eval('info patchlevel'))
        tk._test()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
