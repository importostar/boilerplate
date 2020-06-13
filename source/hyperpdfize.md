---
title: hyperpdfize
date: 2020-05-07
---
Example Python program hyperpdfize.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import os
* from PyQt5.QtCore import *
* from PyQt5.QtGui import *
* from PyQt5.QtWidgets import *
* from PyQt5.QtWebEngineWidgets import *

## Classes

* class HyperPDFizer(QObject):

## Methods

* def __init__(self, input_path, output_path, working_directory=None):
* def run(self):
* def loadFinished(self, ok):
* def pdfPrintingFinished(self, file_path, success):
* def main(argv):

## Code

Example Python PyQt program :

    #!/usr/bin/env python3
    # -*- coding: utf-8 -*-
    # vim: set et sw=4 ts=4  :
    
    # Pythonized from: https://doc.qt.io/qt-5/qtwebengine-webenginewidgets-html2pdf-example.html
    # Differences from the C++ example:
    # - handling local HTML files relative to the current working directory is added.
    # - incognito mode is used.
    # - removed tr() calls from the class.
    # - a few cosemetic changes.
    
    # I could not get rid of the message:
    #     Release of profile requested but WebEnginePage still not deleted. Expect troubles !
    # tried:
    # - moving the contents of main() outside,
    # - making Page a subclass that creates its Profile,
    # - adding deleteLater() to the page,
    # - moving the profile creation into the main,
    # but nothing helped.
    # I could get rid of it by using the default profile (`self.page = QWebEnginePage()`),
    # but I want to have nothing stored when I view a web page to convert it into pdf.
    
    import sys
    import os
    
    from PyQt5.QtCore import *
    from PyQt5.QtGui import *
    from PyQt5.QtWidgets import *
    from PyQt5.QtWebEngineWidgets import *
    
    
    class HyperPDFizer(QObject):
    
        def __init__(self, input_path, output_path, working_directory=None):
            super().__init__()
            self.input  = input_path
            self.output = output_path
            self.cwd    = working_directory
            self.profile = QWebEngineProfile()  # no name given means incognito
            self.page = QWebEnginePage(self.profile, None)
            # self.page = QWebEnginePage()
            self.page.loadFinished.connect(self.loadFinished)
            self.page.pdfPrintingFinished.connect(self.pdfPrintingFinished)
    
        def run(self):
            self.page.load(QUrl.fromUserInput(self.input, self.cwd))
            return QApplication.exec()
    
        def loadFinished(self, ok):
            if not ok:
                print(f"Failed to load URL '{self.input}'", file=sys.stderr, flush=True)
                QCoreApplication.exit(1)
            else:
                self.page.printToPdf(self.output)
    
        def pdfPrintingFinished(self, file_path, success):
            if not success:
                print(f"Failed to print to output file '{file_path}'", file=sys.stderr, flush=True)
                QCoreApplication.exit(1)
            else:
                print(f"Saved '{self.input}' to '{file_path}'")
                QCoreApplication.quit()
    
    
    def main(argv):
        app = QApplication(argv)
        QCoreApplication.setOrganizationName("UnofficiallyPythonizedQtExamples")
        QCoreApplication.setApplicationName("hyperpdfize")
        QCoreApplication.setApplicationVersion('0.1.0+qt'+QT_VERSION_STR)
    
        parser = QCommandLineParser()
        parser.setApplicationDescription(
            QCoreApplication.translate("main", "Converts the web page or HTML file <input> into the PDF file <output>."))
        parser.addHelpOption()
        parser.addVersionOption()
        parser.addPositionalArgument(
            QCoreApplication.translate("main", "<input>"),
            QCoreApplication.translate("main", "Input URL or path for PDF conversion."))
        parser.addPositionalArgument(
            QCoreApplication.translate("main", "<output>"),
            QCoreApplication.translate("main", "Output file name for PDF conversion."))
    
        parser.process(QCoreApplication.arguments())
    
        requiredArguments = parser.positionalArguments()
        if len(requiredArguments) != 2:
            parser.showHelp(1)
    
        converter = HyperPDFizer(requiredArguments[0], requiredArguments[1], os.getcwd())
        return converter.run()
    
    
    if __name__ == '__main__':
        sys.exit(main(sys.argv))
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
