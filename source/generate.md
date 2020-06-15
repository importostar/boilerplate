---
title: generate
date: 2020-05-07
---
Example Python program generate.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import os
* import sys
* import pyblish
* import pyblish_qml
* import pyblish_endpoint
* import PyQt5

## Methods

* def main():

## Code

Example Python PyQt program :

    """Run Pyblish in a clean environment
    
    Usage:
        $ generate.py
        $ run.bat
    
    """
    
    import os
    import sys
    
    
    def main():
        try:
            import pyblish
            import pyblish_qml
            import pyblish_endpoint
            import PyQt5
        except:
            print "Run this in a terminal with access to the Pyblish libraries and PyQt5"
            return
    
        template = r"""@echo off
    
        :: Clear all environment variables
    
        @echo off
        if exist ".\backup_env.bat" del ".\backup_env.bat"
        for /f "tokens=1* delims==" %%a in ('set') do (
        echo set %%a=%%b>> .\backup_env.bat
        set %%a=
        )
    
        :: Set only the bare essentials
    
        set PATH={PyQt5}
        set PATH=%PATH%;{python}
        set PYTHONPATH={pyblish}
        set PYTHONPATH=%PYTHONPATH%;{pyblish_qml}
        set PYTHONPATH=%PYTHONPATH%;{pyblish_endpoint}
        set PYTHONPATH=%PYTHONPATH%;{PyQt5}
    
        set SystemRoot=C:\Windows
    
        :: Run Pyblish
    
        python -m pyblish_qml.app
    
        :: Restore environment
        backup_env.bat
    
        """
    
        values = {}
        for lib in (pyblish, pyblish_qml, pyblish_endpoint, PyQt5):
            values[lib.__name__] = os.path.dirname(os.path.dirname(lib.__file__))
    
        values["python"] = os.path.dirname(sys.executable)
    
        with open("run.bat", "w") as f:
            print "Writing %s" % template.format(**values)
            f.write(template.format(**values))
    
    
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
