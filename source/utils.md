---
title: utils
date: 2020-05-07
---
Example Python program utils.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import os
* import subprocess

## Methods

* def mkdir_p(directory):
* def run_command(cmd, skip=False):
* def run(module, **args):

## Code

Python example

    # coding: utf-8
    import os
    import subprocess
    
    
    def mkdir_p(directory):
        if not os.path.exists(directory):
            os.makedirs(directory)
    
    
    def run_command(cmd, skip=False):
        if not skip:
            print('\n \x1b[2;33;40m' + cmd + '\x1b[0m')
        else:
            print('\n (skiping) \x1b[2;31;40m' + cmd + '\x1b[0m')
        if not skip:
            subprocess.check_call(cmd, shell=True)
    
    
    def run(module, **args):
        cmd = "./scripts/"
        cmd += module.__name__.replace("scripts.", "")
        cmd += ".py"
        for (arg, val) in args.iteritems():
            cmd += " --{} {}".format(arg, val)
    
        if "skip" in args:
            print('\n (skiping) \x1b[2;31;40m' + cmd + '\x1b[0m')
        else:
            print('\n \x1b[2;33;40m' + cmd + '\x1b[0m')
            try:
                module.main(**args)
            except Exception as e:
                print "Error running {} with args {}".format(module.__name__, args)
                raise
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
