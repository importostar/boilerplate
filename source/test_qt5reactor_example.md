---
title: test_qt5reactor_example
date: 2020-05-07
---
Example Python program test_qt5reactor_example.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import time
* import PyQt5
* import pytest
* import twisted.internet.defer
* from twisted.internet import reactor

## Methods

* def test_blue():
* def test_example():
* def qt_event():
* def twisted_event():

## Code

Example Python PyQt program :

    import time
    
    import PyQt5
    import pytest
    import twisted.internet.defer
    
    from twisted.internet import reactor
    
    
    def test_blue():
        instance = PyQt5.QtWidgets.QApplication.instance()
        print('checkpoint', 'test', 'test_blue()', instance)
        assert instance is not None
        o = PyQt5.QtCore.QObject()
        PyQt5.QtCore.qDebug('instance: {}'.format(instance))
        w = PyQt5.QtWidgets.QWidget()
    
    
    @pytest.inlineCallbacks
    def test_example():
        qt_target = 2
        qt_happened = None
    
        def qt_event():
            nonlocal qt_happened
            qt_happened = time.monotonic() - start
    
        timer = PyQt5.QtCore.QTimer()
        timer.setSingleShot(True)
        timer.setInterval(qt_target * 1000)
        timer.timeout.connect(qt_event)
        timer.start()
    
        twisted_target = 3
        twisted_happened = None
    
        def twisted_event():
            nonlocal twisted_happened
            twisted_happened = time.monotonic() - start
    
        reactor.callLater(twisted_target, twisted_event)
    
        done = twisted.internet.defer.Deferred()
        reactor.callLater(5, done.callback, None)
    
        start = time.monotonic()
    
        yield done
    
        assert qt_happened == pytest.approx(qt_target, 0.25)
        assert twisted_happened == pytest.approx(twisted_target, 0.25)
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
