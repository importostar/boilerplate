---
title: setup (1)
date: 2020-05-07
---
Example Python program setup (1).py

## Modules

* from distutils.core import setup
* import sys
* import os
* import matplotlib
* import py2exe

## Methods

* def isSystemDLL(pathname):

## Code

Python example

    # -*- coding: utf-8 -*-
    
    ###
    # $ python setup.py py2exe
    ###
    
    from distutils.core import setup
    import sys
    import os
    import matplotlib
    import py2exe
    
    sys.argv.append('py2exe')
    origIsSystemDLL = py2exe.build_exe.isSystemDLL # save the orginal before we edit it
    def isSystemDLL(pathname):
        # checks if the freetype and ogg dll files are being included
        if os.path.basename(pathname).lower() in ("SDL_ttf.dll","freesansbold.ttf","libfreetype-6.dll", "libogg-0.dll"):
            return 0
        return origIsSystemDLL(pathname) # return the orginal function
    
    py2exe.build_exe.isSystemDLL = isSystemDLL # override the default function with this one
    
    opts = {
        'py2exe': {
            "bundle_files" : 3,
            "compressed" :1,
            "optimize" :2,
            "dll_excludes": ["MSVCP90.dll", "HID.DLL", "w9xpopen.exe"],
            "includes" : [
                "matplotlib.backends",
                "matplotlib.backends.backend_tkagg"
            ],
        }
    }
    
    
    setup(
        data_files=matplotlib.get_py2exe_datafiles(),
        options=opts,
        console=[
            {"script": "main.py"}, #__main__があるやつ
            #{"script": "sub.py"} #必要に応じて増やす
        ],
        zipfile=None
    )
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
