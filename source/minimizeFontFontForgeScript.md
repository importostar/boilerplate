---
title: minimizeFontFontForgeScript
date: 2020-05-07
---
Example Python program minimizeFontFontForgeScript.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import collections
* from io import open
* import sys
* # import warnings
* from PyQt5.QtWidgets import (QDialog, QPushButton, QLineEdit, QLabel,
* from PyQt5.QtCore import Qt

## Classes

* class askSetting(QDialog):

## Methods

* def __init__(self,
* def bye(self, items):

## Code

Example Python PyQt program :

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    import collections
    from io import open
    import sys
    
    # ignore warning
    # import warnings
    # warnings.filterwarnings("ignore")
    
    # can use 3  or 2
    from PyQt5.QtWidgets import (QDialog, QPushButton, QLineEdit, QLabel,
                                 QApplication, QVBoxLayout)
    from PyQt5.QtCore import Qt
    
    
    class askSetting(QDialog):
    
        def __init__(self,
                     app=None,
                     parent=None,
                     items=None):
    
            super(askSetting, self).__init__(parent)
    
            self.app = app
            self.items = items
    
            layout = QVBoxLayout()
    
            self.lineedits = {}
    
            for key in items.keys():
                layout.addWidget(QLabel(key))
                self.lineedits[key] = QLineEdit()
                self.lineedits[key].setText(items[key])
                # enable ime input
                self.lineedits[key].inputMethodQuery(Qt.ImEnabled)
                layout.addWidget(self.lineedits[key])
    
            self.btn = QPushButton('OK', self)
            self.btn.clicked.connect(lambda: (self.bye(items)))
            self.btn.setFocusPolicy(Qt.StrongFocus)
    
            layout.addWidget(self.btn)
    
            self.setLayout(layout)
            self.setWindowTitle(' Setting ')
    
        def bye(self, items):
            for key in self.lineedits.keys():
                self.items[key] = self.lineedits[key].text()
            self.close()
            self.app.exit(1)
    
    
    inFilePrompt = "File to read"
    defaultInFile = "minifyTC"
    
    outFilePrompt = "File to write"
    defaultOutFile = "fontforge.script"
    
    items = collections.OrderedDict()
    items[inFilePrompt] = defaultInFile
    items[outFilePrompt] = defaultOutFile
    
    app = QApplication(sys.argv)
    ask = askSetting(app=app, items=items)
    ask.show()
    rtnCode = app.exec_()
    # If press OK button  rtnCode should be 1
    if rtnCode != 1:
        print('User abort by closing Setting dialog')
        sys.exit
    
    # print(items)
    
    f = open(items[inFilePrompt], 'r', encoding="utf-8")
    # file contents
    # 問
    # 问
    # ie. \w
    ## ie. word
    
    script = open(items[outFilePrompt], 'w', encoding="utf-8")
    script.write(u'#!/usr/local/bin/fontforge\n')
    script.write(u'#\n#Generated from minizeFontFontForgeScript.py\n\n')
    
    
    script.write(u'if ($argc ==2 )\n\tOpen($argv[1])\nendif\n')
    
    script.write(u'SelectNone()\n')
    
    for line in f:
        words = line.encode("raw_unicode_escape").split()
        # words = line.split()
        # print(len(words))
        if len(words) == 1:
            if words[0].startswith(b'\u'):
                ###
                # SelectNone()
                # SelectMore(...)
                # SelectInvert()
                # Clear()
                ###
                print(words[0].decode('unicode_escape'))
                script.write(u'\n#' + words[0].decode('unicode_escape'))
                script.write(
                    u'\nSelectMore(0x' + words[0][2:].decode('utf-8') + u')')
            elif len(words[0]) == 1:
                print(words[0].decode('unicode_escape'))
                script.write(u'\n#' + words[0].decode('unicode_escape'))
                script.write(u'\nSelectMore("' + words[0].decode('utf-8') + u'")')
    
    script.write(u'''
    #if you want distinct eps for each glyph uncomment following')
    #Export("%n.eps")')
    #BitmapsAvail([48])')
    #Export("%n.48.png")')
    
    SelectInvert()')
    Clear()')
    
    Generate('tmp.ttf')")
    
    ##### end of generator\n''')
    script.close()
    
    print(u'Generated as fontforge.script')
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
