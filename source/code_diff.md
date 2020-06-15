---
title: code_diff
date: 2020-05-07
---
Example Python program code_diff.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import difflib
* import os
* import re
* import sys
* from pathlib import Path
* from PyQt5.QtCore import QRegExp
* from PyQt5.QtGui import (QColor,
* from PyQt5.QtWidgets import (QAction,

## Classes

* class DiffHighlighter (QSyntaxHighlighter):
* class Window(QMainWindow):
* class MainWindow(Window):
* class DuplicateWindow(Window):
* class DiffWindow(Window):

## Methods

* def count_texts(text):
* def format(color, style=''):
* def __init__(self, document):
* def highlightBlock(self, text):
* def __init__(self):
* def initUI(self):
* def run(self):
* def autosave(self):
* def done_pressed(self):
* def __init__(self):
* def done_pressed(self, pressed):
* def __init__(self):
* def done_pressed(self):
* def autosave(self):
* def __init__(self):
* def get_diffed_text():

## Code

Example Python PyQt program :

    import difflib
    import os
    import re
    import sys
    from pathlib import Path
    
    from PyQt5.QtCore import QRegExp
    from PyQt5.QtGui import (QColor,
                             QIcon,
                             QSyntaxHighlighter,
                             QTextCharFormat)
    from PyQt5.QtWidgets import (QAction,
                                 QApplication,
                                 QFrame,
                                 QLabel,
                                 QMainWindow,
                                 QPlainTextEdit,
                                 QPushButton,
                                 QTextEdit,
                                 QWidget,
                                 qApp)
    
    ORIG_TEXT = '.__0000__.txt' # save original file here. Change it whatever you like
    DUPL_TEXT = '.__0001__.txt' # save duplicate text here. Change this to anything you like
    
    
    def count_texts(text):
        return len(text.split()), len(text), len(text.splitlines())
    
    
    def format(color, style=''):
        """
        Return a QTextCharFormat with the given attributes.
        """
        _color = QColor()
        _color.setNamedColor(color)
    
        _format = QTextCharFormat()
        _format.setBackground(_color)
    
        return _format
    
    
    # Syntax styles
    STYLES = {
        'plusSymbol': format('magenta'),
        'minusSymbol': format('magenta'),
    }
    
    
    class DiffHighlighter (QSyntaxHighlighter):
        """Syntax highlighter for the diff.
        """
        pSymbol = ['+',]
        mSymbol = ['-',] # this isn't working
            
    
        def __init__(self, document):
            super().__init__(document)
            rules = []
    
            rules += [(r'%s' % o, 0, STYLES['minusSymbol'])
                for o in DiffHighlighter.mSymbol]
    
            self.rules = [(QRegExp(pat + '.*'), index, fmt)
                for (pat, index, fmt) in rules]
    
        def highlightBlock(self, text):
            """Apply syntax highlighting to the given block of text.
            """
            for expression, nth, format in self.rules:
                index = expression.indexIn(text, 0)
                print(expression)
                while index >= 0:
                    index = expression.pos(nth)
                    length = len(expression.cap(nth))
                    self.setFormat(index, length, format)
                    index = expression.indexIn(text, index + length)
    
    
    class Window(QMainWindow):
        '''This is an abstract window that will be used for all other windows.'''
    
        def __init__(self):
            super().__init__()
            self.number = 0
    
            self.initUI()
    
        def initUI(self):
            exit_action = QAction(QIcon('exit.png'), '&Exit', self)
            exit_action.setShortcut('Ctrl+Q')
            exit_action.setStatusTip('Exit Application')
            exit_action.triggered.connect(qApp.quit)
    
            menubar = self.menuBar()
            file_menu = menubar.addMenu('File')
            file_menu.addAction(exit_action)
    
            self.done_button = QPushButton('Done?', self)
            self.done_button.move(250,10)
            self.done_button.clicked[bool].connect(self.done_pressed)
    
            self.square = QFrame(self)
            self.square.setGeometry(150, 20, 100, 100)
    
            self.statusBar().showMessage('Ready')
            self.setGeometry(400, 300, 350, 350)
    
        def run(self):
            self.show()
    
        def autosave(self):
            file_path = Path(__file__)
            save_path = file_path
            with save_path.with_name(self.SAVE_LOC).open('w', encoding='utf8') as f:
                f.write(str(self.text_edit.toPlainText()))
                num_words, num_chars, num_lines  = count_texts(str(self.text_edit.toPlainText()))
    
            self.statusBar().showMessage('Text changed. Autosaving...  ' 
                                         f'{num_words} w   '
                                         f'{num_chars} c   '
                                         '&  '
                                         f'{num_lines} l.  ' )
    
        def done_pressed(self):
            pass
    
    
    class MainWindow(Window):
        def __init__(self):
            super().__init__()
            print(__name__)
            self.SAVE_LOC = ORIG_TEXT  # save text to ORIG_TEXT
    
            self.initUI()
    
            self.original_text_edit_lbl = QLabel('Original text', self)
            self.original_text_edit_lbl.move(80, 70)
        
            self.original_text_edit= QPlainTextEdit(self)
            self.original_text_edit.setPlaceholderText("Enter original text here.")
            self.original_text_edit.setMinimumWidth(285)
            self.original_text_edit.move(50, 100)
            self.original_text_edit.setMinimumSize(100, 200)  # good if you want to insert this into a layout
    
            self.original_text_edit.textChanged.connect(self.autosave)
    
            self.text_edit = self.original_text_edit
    
            self.setWindowTitle('Original Text | CodeDiff')
    
            self.run()
    
        def done_pressed(self, pressed):
            self.original_text_edit.setDisabled(True)  # make text box uneditable
            self.done_button.setDisabled(True)  # disable this button
            self.statusBar().showMessage('Done. Now, you won\'t be able to edit anything in the input box.')
    
            # show other window
            self.duplicate_window = DuplicateWindow()
            self.duplicate_window.show()
    
    
    class DuplicateWindow(Window):
        def __init__(self):
            super().__init__()
            self.SAVE_LOC = DUPL_TEXT # save text to DUPL_TEXT
    
            self.initUI()
    
            self.duplicate_text_edit_lbl = QLabel('Duplicate text', self)
            self.duplicate_text_edit_lbl.move(80, 70)
     
            self.duplicate_text_edit= QPlainTextEdit(self)
            self.duplicate_text_edit.setPlaceholderText("Enter copy of original text here.")
            self.duplicate_text_edit.setMinimumWidth(285)
            self.duplicate_text_edit.move(50, 100)
            self.duplicate_text_edit.setMinimumSize(100, 200)  # good if you want to insert this into a layout
    
            self.duplicate_text_edit.textChanged.connect(self.autosave)
    
            self.text_edit = self.duplicate_text_edit
    
            self.setWindowTitle('Duplicate Text | CodeDiff')
    
            self.setGeometry(30, 300, 350, 350)
    
            self.run()
    
        def done_pressed(self):
            self.diff_window = DiffWindow()
            self.diff_window.show()
    
        def autosave(self):
            super().autosave()
            try:
                self.diff_window.diff_text.setText('\n'.join(get_diffed_text()))
            except:
                pass
    
    
    class DiffWindow(Window):
        def __init__(self):
            super().__init__()
            super().initUI()        
    
            self.diff_text_lbl = QLabel('Diff', self)
            self.diff_text_lbl.move(80, 70)
     
            self.diff_text= QTextEdit(self)
            highlight = DiffHighlighter(self.diff_text.document())
    
            self.diff_text.append('\n'.join(get_diffed_text()))
            self.diff_text.setMinimumWidth(285)
            self.diff_text.setMinimumSize(100, 200)  # good if you want to insert this into a layout
            self.diff_text.move(50, 100)
            self.diff_text.setReadOnly(True)
    
            self.setGeometry(300, 300, 350, 350)
    
            self.done_button.setDisabled(True)
    
            self.setWindowTitle('Diff Text | CodeDiff')
    
            self.setGeometry(800, 300, 350, 350)
    
            self.run()
    
    
    def get_diffed_text():
        o_f = Path(__file__).with_name(ORIG_TEXT).open('r', encoding='utf8')
        d_f = Path(__file__).with_name(DUPL_TEXT).open('r', encoding='utf8')
        d = difflib.Differ()
        diff = d.compare(o_f.read().splitlines(), d_f.read().splitlines())
        return diff
    
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        main_window = MainWindow()
        main_window.show()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
