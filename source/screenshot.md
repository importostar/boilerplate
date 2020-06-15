---
title: screenshot
date: 2020-05-07
---
Example Python program screenshot.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from os.path import basename
* from os.path import dirname
* from os.path import join
* import sys
* from PyQt5.QtCore import Qt
* from PyQt5.QtCore import QUrl
* from PyQt5.QtCore import QTimer
* from PyQt5.QtGui import QPixmap
* from PyQt5.QtWebEngineWidgets import QWebEngineView
* from PyQt5.QtWidgets import QApplication

## Methods

* def finished(browser, url, wait_ms):
* def inner(result):
* def capture(browser, fname):

## Code

Example Python PyQt program :

    from os.path import basename
    from os.path import dirname
    from os.path import join
    import sys
    
    from PyQt5.QtCore import Qt
    from PyQt5.QtCore import QUrl
    from PyQt5.QtCore import QTimer
    from PyQt5.QtGui import QPixmap
    from PyQt5.QtWebEngineWidgets import QWebEngineView
    from PyQt5.QtWidgets import QApplication
    
    
    def finished(browser, url, wait_ms):
        def inner(result):
            if result and browser.url().toString() == url:
                fname = join(dirname(__file__), basename(url) + ".png")
                QTimer.singleShot(wait_ms, lambda: capture(browser, fname))
        return inner
    
    
    def capture(browser, fname):
        size = browser.contentsRect()
        img = QPixmap(size.width(), size.height())
        browser.render(img)
        img.save(fname)
        browser.close()
    
    
    try:
        size, url = [int(s) for s in sys.argv[1:3]], sys.argv[3]
    except (IndexError, ValueError):
        print("Usage: %s <window_w> <window_h> <url>" % sys.argv[0], file=sys.stdout)
        sys.exit(1)
    
    app = QApplication(sys.argv)
    
    browser = QWebEngineView()
    browser.setAttribute(Qt.WA_DontShowOnScreen, True)
    browser.setAttribute(Qt.WA_DeleteOnClose, True)
    browser.resize(*size)
    browser.show()
    browser.load(QUrl(url))
    browser.loadFinished.connect(finished(browser, url, 3000))
    sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
