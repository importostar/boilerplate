---
title: webView
date: 2020-05-07
---
Example Python program webView.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from cu2qu.defcon import font_to_quadratic
* from fontTools.feaLib.error import FeatureLibError
* from io import BytesIO
* from PyQt5.QtGui import QFontDatabase
* from PyQt5.QtWebEngineWidgets import QWebEngineView
* from PyQt5.QtWebKit import QWebView

## Classes

* class WebEngineFontView(QWebEngineView):

## Methods

* def __init__(self, parent=None):
* def closeEvent(self, event):
* def _extractPSName(self, font):
* def _fontChanged(self, notification):
* def updateFont(self):
* def updateHtml(self, psName):

## Code

Example Python PyQt program :

    from cu2qu.defcon import font_to_quadratic
    from fontTools.feaLib.error import FeatureLibError
    from io import BytesIO
    from PyQt5.QtGui import QFontDatabase
    try:
        # Chromium
        from PyQt5.QtWebEngineWidgets import QWebEngineView
    except ImportError:
        # WebKit
        from PyQt5.QtWebKit import QWebView
        QWebEngineView = QWebView
    
    class WebEngineFontView(QWebEngineView):
        def __init__(self, parent=None):
            super().__init__(parent)
            self._font = CurrentFont()
            self._font.addObserver(
                self, "_fontChanged", "Font.Changed")
            self._fontId = None
            self.updateFont()
        
        def closeEvent(self, event):
            self._font.removeObserver(self, "Font.Changed")
            event.accept()
        
        # drawbot, edited
        def _extractPSName(self, font):
            psName = font["name"].getName(6, 1, 0)
            if psName is None:
                psName = font["name"].getName(6, 3, 1)
            return psName
        
        def _fontChanged(self, notification):
            self.updateFont()
        
        def updateFont(self):
            font_to_quadratic(self._font)
            try:
                otf = self._font.getRepresentation(
                    "defconQt.QuadraticTTFont")
            except FeatureLibError as e:
                traceback.print_exc()
                print(e.location)
                return
            stream = BytesIO()
            otf.save(stream)
            id = QFontDatabase.addApplicationFontFromData(
                stream.getvalue())
            if id == -1:
                return
            if self._fontId is not None:
                QFontDatabase.removeApplicationFont(
                    self._fontId)
            psName = self._extractPSName(otf)
            if psName is None:
                return
            self._fontId = id
            self.updateHtml(psName)
        
        def updateHtml(self, psName):
            html = """
    <head>
        <style>
            html {
                font-family: %s;
            }
        <style>
    </head>
    <body>
       Grumpy wizards make toxic brew for the evil Queen and Jack. A quick movement of the enemy will jeopardize six gunboats. The job of waxing linoleum frequently peeves chintzy kids. My girl wove six dozen plaid jackets before she quit. Twelve ziggurats quickly jumped a finch box.
    </body>
            """ % psName
            self.setHtml(html)
    
    webView = WebEngineFontView()
    webView.show()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
