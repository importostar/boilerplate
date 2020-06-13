---
title: pyqt5_scraper (1)
date: 2020-05-07
---
Example Python program pyqt5_scraper (1).py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* # standard imports
* import sys
* # third-party imports
* import requests
* from bs4 import BeautifulSoup
* from pyvirtualdisplay import Display
* from PyQt5.QtWebKitWidgets import QWebPage
* from PyQt5.QtWidgets import QApplication

## Classes

* class Render(QWebPage):

## Methods

* def __init__(self, html):
* def _loadFinished(self, result):

## Code

Example Python PyQt program :

    #!/usr/bin/env python3
    # -*- coding: utf-8 -*-
    """
    Sample scraper script
    
    See: https://impythonist.wordpress.com/2015/01/06/ultimate-guide-for-scraping-javascript-rendered-web-pages/
    """
    
    # standard imports
    import sys
    
    # third-party imports
    import requests
    from bs4 import BeautifulSoup
    from pyvirtualdisplay import Display
    from PyQt5.QtWebKitWidgets import QWebPage
    from PyQt5.QtWidgets import QApplication
    
    
    class Render(QWebPage):
        """Render HTML with PyQt5 WebKit."""
    
        def __init__(self, html):
            self.html = None
            self.app = QApplication(sys.argv)
            QWebPage.__init__(self)
            self.loadFinished.connect(self._loadFinished)
            self.mainFrame().setHtml(html)
            self.app.exec_()
    
        def _loadFinished(self, result):
            self.html = self.mainFrame().toHtml()
            self.app.quit()
    
    
    url = 'https://impythonist.wordpress.com/2015/01/06/ultimate-guide-for-scraping-javascript-rendered-web-pages/'
    
    # get the raw HTML
    source_html = requests.get(url).text
    
    # return the JavaScript rendered HTML
    with Display(visible=0, size=(800, 600)):
        rendered_html = Render(source_html).html
    
    # get the BeautifulSoup
    soup = BeautifulSoup(rendered_html, 'html.parser')
    
    print('title is %r' % soup.select_one('title').text)
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
