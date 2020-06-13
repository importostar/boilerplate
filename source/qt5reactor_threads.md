---
title: qt5reactor_threads
date: 2020-05-07
---
Example Python program qt5reactor_threads.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import qt5reactor
* import sys
* import time
* import twisted
* from PyQt5 import QtCore

## Methods

* def thread():
* def quit():

## Code

Example Python PyQt program :

    import qt5reactor
    import sys
    import time
    import twisted
    
    from PyQt5 import QtCore
    
    
    def thread():
        print('threading')
        time.sleep(1)
        print('done threading')
    
    
    def quit():
        print('quitting')
    
        # TODO: _stopThreadPool() should not be necessary but otherwise
        #       it hangs on quit.  Killing results in:
        #
        # Exception ignored in: <module 'threading' from '/usr/lib/python3.5/threading.py'>
        # Traceback (most recent call last):
        #   File "/usr/lib/python3.5/threading.py", line 1288, in _shutdown
        #     t.join()
        #   File "/usr/lib/python3.5/threading.py", line 1054, in join
        #     self._wait_for_tstate_lock()
        #   File "/usr/lib/python3.5/threading.py", line 1070, in _wait_for_tstate_lock
        #     elif lock.acquire(block, timeout):
        # KeyboardInterrupt
    
        twisted.internet.reactor._stopThreadPool()
    
        app.quit()
        print('already quit')
    
    
    app = QtCore.QCoreApplication(sys.argv)
    
    qt5reactor.install()
    
    # TODO: getThreadPool().start() should not be required but otherwise
    #       it hangs without running thread()
    twisted.internet.reactor.getThreadPool().start()
    
    d = twisted.internet.threads.deferToThread(thread)
    d.addCallback(lambda _: quit())
    
    sys.exit(app.exec())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
