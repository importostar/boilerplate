---
title: python exec2.original
date: 2020-05-07
---
Example Python program python-exec2.original.py

## Modules

* from __future__ import with_statement
* import os, os.path, sys
* from epython import EPYTHON
* import tokenize

## Code

Python example

    #!/usr/lib/python-exec/python-exec2-c
    # vim:fileencoding=utf-8:ft=python
    # (c) 2012 Michał Górny
    # Released under the terms of the 2-clause BSD license.
    #
    # This is not the script you are looking for. This is just a wrapper.
    # The actual scripts of this application were installed with -python*,
    # -pypy* or -jython* suffixes. You are most likely looking for one
    # of those.
    
    from __future__ import with_statement
    import os, os.path, sys
    
    try:
            from epython import EPYTHON
    except ImportError:
            EPYTHON = os.path.basename(sys.executable)
            if '' and EPYTHON.endswith(''):
                    EPYTHON = EPYTHON[:-len('')]
    
    # In the loop:
    # sys.argv[0] keeps the 'bare' name
    # __file__ keeps the 'full' name
    
    while True:
            __file__ = os.path.join('/usr/lib/python-exec', EPYTHON,
                            os.path.basename(sys.argv[0]))
    
            try:
                    kwargs = {}
                    if sys.version_info[0] >= 3:
                            import tokenize
    
                            # need to provide encoding
                            with open(__file__, 'rb') as f:
                                    kwargs['encoding'] = tokenize.detect_encoding(f.readline)[0]
    
                    with open(__file__, 'r', **kwargs) as f:
                            data = f.read()
            except IOError:
                    # follow symlinks (if supported)
                    try:
                            sys.argv[0] = os.path.join(os.path.dirname(sys.argv[0]),
                                            os.readlink(sys.argv[0]))
                    except (OSError, AttributeError):
                            # no more symlinks? then it's time to fail.
                            sys.stderr.write('This Python implementation (%s) is not supported by the script.\n'
                                            % EPYTHON)
                            sys.exit(127)
            else:
                    break
    
    sys.argv[0] = __file__
    exec(data)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
