---
title: genFontForgeScript
date: 2020-05-07
---
Example Python program genFontForgeScript.py
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
    defaultInFile = "extendStoTC"
    
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
    # 問 问
    # ie. \w\s\w
    # ie. word space word
    
    script = open(items[outFilePrompt], 'w', encoding="utf-8")
    script.write(u'#!/usr/local/bin/fontforge\n')
    script.write(u'#\n#Generated from genFontForgeScript.py\n\n')
    script.write(u'if ($argc ==2 )\n\tOpen($argv[1])\nendif\n')
    # a = open('a.txt', 'w', encoding="utf-8")
    
    for line in f:
        words = line.encode("raw_unicode_escape").split()
        # words = line.split()
        # print(len(words))
        if len(words) == 2:
            if words[0] == words[1]:
                pass
            elif words[0].startswith(b'\u') and words[1].startswith(b'\u'):
                ###
                # Select(0x570b)
                # CopyReference()
                # Select(0x56fd)
                # Paste()
                ###
                print(words[0].decode('unicode_escape') +
                      u' -> ' +
                      words[1].decode('unicode_escape'))
                # a.write(u'\n' + words[0].decode('unicode_escape'))
                # a.erite(u' ' + words[1].decode('unicode_escape'))
                script.write(u'\n#' + words[0].decode('unicode_escape'))
                script.write(u'\nSelect(0x' + words[0][2:].decode('utf-8') + u')')
                script.write(u'\nCopyReference()')
                script.write(u'\n#' + words[1].decode('unicode_escape'))
                script.write(u'\nSelect(0x' + words[1][2:].decode('utf-8') + u')')
                script.write(u'\nPaste()')
    # a.write(u'\n')
    # a.close()
    script.write(u"\n\nGenerate('tmp.ttf')")
    script.write(u'\n\n##### end of generator\n')
    script.close()
    
    print(u'Generated as fontforge.script')
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
