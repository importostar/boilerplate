---
title: editor_qt5
date: 2020-05-07
---
Example Python program editor_qt5.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5.QtWidgets import QMainWindow, QApplication, QWidget, QTabWidget, QVBoxLayout, QPlainTextEdit
* from PyQt5.QtGui import QIcon, QColor, QTextCharFormat, QFont, QSyntaxHighlighter
* from PyQt5.QtCore import pyqtSlot, QRegExp
* "for", "from", "global", "if", "import", "in",

## Classes

* class ResaltadorPython(QSyntaxHighlighter):
* class Notebook(QWidget):
* class App(QMainWindow):

## Methods

* def formatear(color, estilo=""):
* def __init__(self, document):
* def highlightBlock(self, text):
* def match_multiline(self, text, delimiter, in_state, style):
* def __init__(self, parent):   
* def __init__(self):

## Code

Example Python PyQt program :

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    import sys
    from PyQt5.QtWidgets import QMainWindow, QApplication, QWidget, QTabWidget, QVBoxLayout, QPlainTextEdit
    from PyQt5.QtGui import QIcon, QColor, QTextCharFormat, QFont, QSyntaxHighlighter
    from PyQt5.QtCore import pyqtSlot, QRegExp
    
    
    
    def formatear(color, estilo=""):
        """Return a QTextCharFormat with the given attributes."""
        qcolor = QColor()
        qcolor.setNamedColor(color)
    
        formato = QTextCharFormat()
        formato.setForeground(qcolor)
    
        if "bold" in estilo:
            formato.setFontWeight(QFont.Bold)
    
        if "italic" in estilo:
            formato.setFontItalic(True)
    
        return formato
    
    
    ESTILOS = {
        "keyword": formatear("blue"),
        "operator": formatear("red"),
        "brace": formatear("darkGray"),
        "defclass": formatear("black", "bold"),
        "string": formatear("magenta"),
        "string2": formatear("darkMagenta"),
        "comment": formatear("darkGreen", "italic"),
        "self": formatear("black", "italic"),
        "numbers": formatear("brown"),
    }
    
    
    class ResaltadorPython(QSyntaxHighlighter):
    
        def __init__(self, document):
            QSyntaxHighlighter.__init__(self, document)
    
            self.keywords = [
                "and", "assert", "break", "class", "continue", "def",
                "del", "elif", "else", "except", "exec", "finally",
                "for", "from", "global", "if", "import", "in",
                "is", "lambda", "not", "or", "pass", "print",
                "raise", "return", "try", "while", "yield",
                "None", "True", "False",
            ]
    
            self.operadores = [
                "=",
                "==", "!=", "<", "<=", ">", ">=",
                "\+", "-", "\*", "/", "//", "\%", "\*\*",
                "\+=", "-=", "\*=", "/=", "\%=",
                "\^", "\|", "\&", "\~", ">>", "<<",
            ]
    
            self.parentesis = [
                "\{", "\}", "\(", "\)", "\[", "\]",
            ]
    
            self.tri_single = (QRegExp("'''"), 1, ESTILOS['string2'])
            self.tri_double = (QRegExp('"""'), 2, ESTILOS['string2'])
    
            # Todas las reglas de sintaxis de python
            rules = []
    
            rules += [(r"\b%s\b" % w, 0, ESTILOS["keyword"]) for w in self.keywords]
            rules += [(r"%s" % o, 0, ESTILOS["operator"]) for o in self.operadores]
            rules += [(r"%s" % b, 0, ESTILOS["brace"]) for b in self.parentesis]
    
            rules += [
                # self
                (r"\bself\b", 0, ESTILOS["self"]),
    
                # Double-quoted string, possibly containing escape sequences
                (r'"[^"\\]*(\\.[^"\\]*)*', 0, ESTILOS["string"]),
    
                # "def" followed by an identifier
                (r"\bdef\b\s*(\w+)", 1, ESTILOS["defclass"]),
                # "class" followed by an identifier
                (r"\bclass\b\s*(\w+)", 1, ESTILOS["defclass"]),
    
                # From "#" until a newline
                (r"#[^\n]*", 0, ESTILOS["comment"]),
    
                # Numeric literals
                (r"\b[+-]?[0-9]+[lL]?\b", 0, ESTILOS["numbers"]),
                (r"\b[+-]?0[xX][0-9A-Fa-f]+[lL]?\b", 0, ESTILOS["numbers"]),
                (r"\b[+-]?[0-9]+(?:\.[0-9]+)?(?:[eE][+-]?[0-9]+)?\b", 0, ESTILOS["numbers"]),
            ]
    
            # Build a QRegExp for each pattern
            self.rules = [(QRegExp(pat), index, fmt) for (pat, index, fmt) in rules]
    
        def highlightBlock(self, text):
            """Apply syntax highlighting to the given block of text."""
            # Do other syntax formatting
            for expression, nth, format in self.rules:
                index = expression.indexIn(text, 0)
    
                while index >= 0:
                    # We actually want the index of the nth match
                    index = expression.pos(nth)
                    length = len(expression.cap(nth))
                    self.setFormat(index, length, format)
                    index = expression.indexIn(text, index + length)
    
            self.setCurrentBlockState(0)
    
            # Do multi-line strings
            in_multiline = self.match_multiline(text, *self.tri_single)
            if not in_multiline:
                in_multiline = self.match_multiline(text, *self.tri_double)
    
    
        def match_multiline(self, text, delimiter, in_state, style):
            # If inside triple-single quotes, start at 0
            if self.previousBlockState() == in_state:
                start = 0
                add = 0
            # Otherwise, look for the delimiter on this line
            else:
                start = delimiter.indexIn(text)
                # Move past this match
                add = delimiter.matchedLength()
    
            # As long as there"s a delimiter match on this line...
            while start >= 0:
                # Look for the ending delimiter
                end = delimiter.indexIn(text, start + add)
                # Ending delimiter on this line?
                if end >= add:
                    length = end - start + add + delimiter.matchedLength()
                    self.setCurrentBlockState(0)
                # No; multi-line string
                else:
                    self.setCurrentBlockState(in_state)
                    length = text.length() - start + add
    
                # Apply formatting
                self.setFormat(start, length, style)
                # Look for the next match
                start = delimiter.indexIn(text, start + length)
    
            # Return True if still inside a multi-line string, False otherwise
            if self.currentBlockState() == in_state:
                return True
    
            else:
                return False
    
    
    class Notebook(QWidget):        
    
        def __init__(self, parent):   
            QWidget.__init__(self, parent)
    
            self.layout = QVBoxLayout(self)
    
            # Initialize tab screen
            self.notebook = QTabWidget()
            self.notebook.resize(300,200)
    
            for x in range(0, 5):
                tab = QWidget()
                layout = QVBoxLayout(tab)
                self.notebook.addTab(tab, "Tab %d" % x)
    
                editor = QPlainTextEdit()
                highlight = ResaltadorPython(editor.document())
                layout.addWidget(editor)
                tab.setLayout(layout)
    
                if x == 0:
                    archivo = open("archivo.py")
                    texto = archivo.read()
                    editor.setPlainText(texto)
    
            # Add tabs to widget        
            self.layout.addWidget(self.notebook)
            self.setLayout(self.layout)
    
    
    class App(QMainWindow):
    
        def __init__(self):
            super().__init__()
            self.title = "PyQt5 notebook"
            self.left = 0
            self.top = 0
            self.width = 300
            self.height = 200
            self.setWindowTitle(self.title)
            self.setGeometry(self.left, self.top, self.width, self.height)
    
            self.notebook = Notebook(self)
            self.setCentralWidget(self.notebook)
    
            self.show()
    
    
    
    if __name__ == "__main__":
        app = QApplication(sys.argv)
        ex = App()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
