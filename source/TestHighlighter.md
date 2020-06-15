---
title: TestHighlighter
date: 2020-05-07
---
Example Python program TestHighlighter.py
This program creates a PyQt GUI

## Modules

* import PyQt5 as PyQt
* from PyQt5.QtCore import Qt, QRect, QRegExp
* from PyQt5.QtWidgets import QWidget, QTextEdit, QPlainTextEdit
* from PyQt5.QtGui import (QColor, QPainter, QFont, QSyntaxHighlighter,
* # imports required PyQt modules
* from PyQt5.QtWidgets import QApplication
* import sys

## Classes

* class CHighlighter(QSyntaxHighlighter):
* class XMLHighlighter(QSyntaxHighlighter):
* class QCodeEditor(QPlainTextEdit):
* class NumberBar(QWidget):

## Methods

* def __init__(self, parent=None):
* def highlightBlock(self, text):
* def __init__(self, parent=None):
* def highlightBlock(self, text):
* def __init__(self, editor):
* def paintEvent(self, event):
* def getWidth(self):
* def updateWidth(self):
* def updateContents(self, rect, scroll):
* def __init__(self, DISPLAY_LINE_NUMBERS=True, HIGHLIGHT_CURRENT_LINE=True,
* def resizeEvent(self, *e):
* def highligtCurrentLine(self):
* def run_test():

## Code

Example Python PyQt program :

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    
    
    import PyQt5 as PyQt
    from PyQt5.QtCore import Qt, QRect, QRegExp
    from PyQt5.QtWidgets import QWidget, QTextEdit, QPlainTextEdit
    from PyQt5.QtGui import (QColor, QPainter, QFont, QSyntaxHighlighter,
                             QTextFormat, QTextCharFormat)
    
    
    # classes definition
    
    class CHighlighter(QSyntaxHighlighter):
        def __init__(self, parent=None):
            super(CHighlighter, self).__init__(parent)
    
            keywordFormat = QTextCharFormat()
            keywordFormat.setForeground(Qt.darkBlue)
            keywordFormat.setFontWeight(QFont.Bold)
    
            keywordPatterns = ["\\bchar\\b", "\\bclass\\b", "\\bconst\\b",
                               "\\bdouble\\b", "\\benum\\b", "\\bexplicit\\b", "\\bfriend\\b",
                               "\\binline\\b", "\\bint\\b", "\\blong\\b", "\\bnamespace\\b",
                               "\\boperator\\b", "\\bprivate\\b", "\\bprotected\\b",
                               "\\bpublic\\b", "\\bshort\\b", "\\bsignals\\b", "\\bsigned\\b",
                               "\\bslots\\b", "\\bstatic\\b", "\\bstruct\\b",
                               "\\btemplate\\b", "\\btypedef\\b", "\\btypename\\b",
                               "\\bunion\\b", "\\bunsigned\\b", "\\bvirtual\\b", "\\bvoid\\b",
                               "\\bvolatile\\b"]
    
            self.highlightingRules = [(QRegExp(pattern), keywordFormat)
                                      for pattern in keywordPatterns]
    
            classFormat = QTextCharFormat()
            classFormat.setFontWeight(QFont.Bold)
            classFormat.setForeground(Qt.darkMagenta)
            self.highlightingRules.append((QRegExp("\\bQ[A-Za-z]+\\b"), classFormat))
    
            singleLineCommentFormat = QTextCharFormat()
            singleLineCommentFormat.setForeground(Qt.red)
            self.highlightingRules.append((QRegExp("//[^\n]*"), singleLineCommentFormat))
    
            self.multiLineCommentFormat = QTextCharFormat()
            self.multiLineCommentFormat.setForeground(Qt.red)
    
            quotationFormat = QTextCharFormat()
            quotationFormat.setForeground(Qt.darkGreen)
            self.highlightingRules.append((QRegExp("\".*\""), quotationFormat))
    
            functionFormat = QTextCharFormat()
            functionFormat.setFontItalic(True)
            functionFormat.setForeground(Qt.blue)
            self.highlightingRules.append((QRegExp("\\b[A-Za-z0-9_]+(?=\\()"), functionFormat))
    
            self.commentStartExpression = QRegExp("/\\*")
            self.commentEndExpression = QRegExp("\\*/")
    
        def highlightBlock(self, text):
            for pattern, format in self.highlightingRules:
                expression = QRegExp(pattern)
                index = expression.indexIn(text)
                while index >= 0:
                    length = expression.matchedLength()
                    self.setFormat(index, length, format)
                    index = expression.indexIn(text, index + length)
    
            self.setCurrentBlockState(0)
    
            startIndex = 0
            if self.previousBlockState() != 1:
                startIndex = self.commentStartExpression.indexIn(text)
    
            while startIndex >= 0:
                endIndex = self.commentEndExpression.indexIn(text, startIndex)
    
                if endIndex == -1:
                    self.setCurrentBlockState(1)
                    commentLength = len(text) - startIndex
                else:
                    commentLength = endIndex - startIndex + self.commentEndExpression.matchedLength()
    
                self.setFormat(startIndex, commentLength,
                               self.multiLineCommentFormat)
                startIndex = self.commentStartExpression.indexIn(text, startIndex + commentLength)
    
    
    class XMLHighlighter(QSyntaxHighlighter):
        '''
        Class for highlighting xml text inherited from QSyntaxHighlighter
        reference:
            http://www.yasinuludag.com/blog/?p=49
    
        '''
    
        def __init__(self, parent=None):
    
            super(XMLHighlighter, self).__init__(parent)
    
            self.highlightingRules = []
    
            xmlElementFormat = QTextCharFormat()
            xmlElementFormat.setForeground(QColor("#000070"))  # blue
            self.highlightingRules.append((QRegExp("\\b[A-Za-z0-9_]+(?=[\s/>])"), xmlElementFormat))
    
            xmlAttributeFormat = QTextCharFormat()
            xmlAttributeFormat.setFontItalic(True)
            xmlAttributeFormat.setForeground(QColor("#177317"))  # green
            self.highlightingRules.append((QRegExp("\\b[A-Za-z0-9_]+(?=\\=)"), xmlAttributeFormat))
            self.highlightingRules.append((QRegExp("="), xmlAttributeFormat))
    
            self.valueFormat = QTextCharFormat()
            self.valueFormat.setForeground(QColor("#e35e00"))  # orange
            self.valueStartExpression = QRegExp("\"")
            self.valueEndExpression = QRegExp("\"(?=[\s></])")
    
            singleLineCommentFormat = QTextCharFormat()
            singleLineCommentFormat.setForeground(QColor("#a0a0a4"))  # grey
            self.highlightingRules.append((QRegExp("<!--[^\n]*-->"), singleLineCommentFormat))
    
            textFormat = QTextCharFormat()
            textFormat.setForeground(QColor("#000000"))  # black
            # (?<=...)  - lookbehind is not supported
            self.highlightingRules.append((QRegExp(">(.+)(?=</)"), textFormat))
    
            keywordFormat = QTextCharFormat()
            keywordFormat.setForeground(QColor("#000070"))  # blue
            keywordFormat.setFontWeight(QFont.Bold)
            keywordPatterns = ["\\b?xml\\b", "/>", ">", "<", "</"]
            self.highlightingRules += [(QRegExp(pattern), keywordFormat)
                                       for pattern in keywordPatterns]
    
        # VIRTUAL FUNCTION WE OVERRIDE THAT DOES ALL THE COLLORING
        def highlightBlock(self, text):
            # for every pattern
            for pattern, format in self.highlightingRules:
                # Create a regular expression from the retrieved pattern
                expression = QRegExp(pattern)
                # Check what index that expression occurs at with the ENTIRE text
                index = expression.indexIn(text)
                # While the index is greater than 0
                while index >= 0:
                    # Get the length of how long the expression is true, set the format from the start to the length with the text format
                    length = expression.matchedLength()
                    self.setFormat(index, length, format)
                    # Set index to where the expression ends in the text
                    index = expression.indexIn(text, index + length)
    
                    # HANDLE QUOTATION MARKS NOW.. WE WANT TO START WITH " AND END WITH ".. A THIRD " SHOULD NOT CAUSE THE WORDS INBETWEEN SECOND AND THIRD TO BE COLORED
            self.setCurrentBlockState(0)
            startIndex = 0
            if self.previousBlockState() != 1:
                startIndex = self.valueStartExpression.indexIn(text)
            while startIndex >= 0:
                endIndex = self.valueEndExpression.indexIn(text, startIndex)
                if endIndex == -1:
                    self.setCurrentBlockState(1)
                    commentLength = len(text) - startIndex
                else:
                    commentLength = endIndex - startIndex + self.valueEndExpression.matchedLength()
                self.setFormat(startIndex, commentLength, self.valueFormat)
                startIndex = self.valueStartExpression.indexIn(text, startIndex + commentLength);
    
    
    class QCodeEditor(QPlainTextEdit):
        '''
        QCodeEditor inherited from QPlainTextEdit providing:
    
            numberBar - set by DISPLAY_LINE_NUMBERS flag equals True
            curent line highligthing - set by HIGHLIGHT_CURRENT_LINE flag equals True
            setting up QSyntaxHighlighter
        references:
            https://john.nachtimwald.com/2009/08/19/better-qplaintextedit-with-line-numbers/
            http://doc.qt.io/qt-5/qtwidgets-widgets-codeeditor-example.html
    
        '''
    
        class NumberBar(QWidget):
            '''class that defines textEditor numberBar'''
    
            def __init__(self, editor):
                QWidget.__init__(self, editor)
    
                self.editor = editor
                self.editor.blockCountChanged.connect(self.updateWidth)
                self.editor.updateRequest.connect(self.updateContents)
                self.font = QFont()
                self.numberBarColor = QColor("#e8e8e8")
    
            def paintEvent(self, event):
    
                painter = QPainter(self)
                painter.fillRect(event.rect(), self.numberBarColor)
    
                block = self.editor.firstVisibleBlock()
    
                # Iterate over all visible text blocks in the document.
                while block.isValid():
                    blockNumber = block.blockNumber()
                    block_top = self.editor.blockBoundingGeometry(block).translated(self.editor.contentOffset()).top()
    
                    # Check if the position of the block is out side of the visible area.
                    if not block.isVisible() or block_top >= event.rect().bottom():
                        break
    
                    # We want the line number for the selected line to be bold.
                    if blockNumber == self.editor.textCursor().blockNumber():
                        self.font.setBold(True)
                        painter.setPen(QColor("#000000"))
                    else:
                        self.font.setBold(False)
                        painter.setPen(QColor("#717171"))
                    painter.setFont(self.font)
    
                    # Draw the line number right justified at the position of the line.
                    paint_rect = QRect(0, block_top, self.width(), self.editor.fontMetrics().height())
                    painter.drawText(paint_rect, Qt.AlignRight, str(blockNumber + 1))
    
                    block = block.next()
    
                painter.end()
    
                QWidget.paintEvent(self, event)
    
            def getWidth(self):
                count = self.editor.blockCount()
                width = self.fontMetrics().width(str(count)) + 10
                return width
    
            def updateWidth(self):
                width = self.getWidth()
                if self.width() != width:
                    self.setFixedWidth(width)
                    self.editor.setViewportMargins(width, 0, 0, 0)
    
            def updateContents(self, rect, scroll):
                if scroll:
                    self.scroll(0, scroll)
                else:
                    self.update(0, rect.y(), self.width(), rect.height())
    
                if rect.contains(self.editor.viewport().rect()):
                    fontSize = self.editor.currentCharFormat().font().pointSize()
                    self.font.setPointSize(fontSize)
                    self.font.setStyle(QFont.StyleNormal)
                    self.updateWidth()
    
        def __init__(self, DISPLAY_LINE_NUMBERS=True, HIGHLIGHT_CURRENT_LINE=True,
                     SyntaxHighlighter=None, *args):
            '''
            Parameters
            ----------
            DISPLAY_LINE_NUMBERS : bool
                switch on/off the presence of the lines number bar
            HIGHLIGHT_CURRENT_LINE : bool
                switch on/off the current line highliting
            SyntaxHighlighter : QSyntaxHighlighter
                should be inherited from QSyntaxHighlighter
    
            '''
            super(QCodeEditor, self).__init__()
    
            self.setFont(QFont("Ubuntu Mono", 11))
            self.setLineWrapMode(QPlainTextEdit.NoWrap)
    
            self.DISPLAY_LINE_NUMBERS = DISPLAY_LINE_NUMBERS
    
            if DISPLAY_LINE_NUMBERS:
                self.number_bar = self.NumberBar(self)
    
            if HIGHLIGHT_CURRENT_LINE:
                self.currentLineNumber = None
                self.currentLineColor = self.palette().alternateBase()
                # self.currentLineColor = QColor("#e8e8e8")
                self.cursorPositionChanged.connect(self.highligtCurrentLine)
    
            if SyntaxHighlighter is not None:  # add highlighter to textdocument
                self.highlighter = SyntaxHighlighter(self.document())
    
        def resizeEvent(self, *e):
            '''overload resizeEvent handler'''
    
            if self.DISPLAY_LINE_NUMBERS:  # resize number_bar widget
                cr = self.contentsRect()
                rec = QRect(cr.left(), cr.top(), self.number_bar.getWidth(), cr.height())
                self.number_bar.setGeometry(rec)
    
            QPlainTextEdit.resizeEvent(self, *e)
    
        def highligtCurrentLine(self):
            newCurrentLineNumber = self.textCursor().blockNumber()
            if newCurrentLineNumber != self.currentLineNumber:
                self.currentLineNumber = newCurrentLineNumber
                hi_selection = QTextEdit.ExtraSelection()
                hi_selection.format.setBackground(self.currentLineColor)
                hi_selection.format.setProperty(QTextFormat.FullWidthSelection, True)
                hi_selection.cursor = self.textCursor()
                hi_selection.cursor.clearSelection()
                self.setExtraSelections([hi_selection])
    
            ##############################################################################
    
    
    if __name__ == '__main__':
    
        # TESTING
    
        def run_test():
    
            # imports required PyQt modules
            from PyQt5.QtWidgets import QApplication
    
            import sys
    
            app = QApplication([])
    
            editor = QCodeEditor(DISPLAY_LINE_NUMBERS=True,
                                 HIGHLIGHT_CURRENT_LINE=True,
                                 SyntaxHighlighter=CHighlighter)
    
            text = '''  <dialog id="voice-overlay-dialog" class="overlay-dialog">
        <div id="voice-overlay" class="overlay-hidden">
          <button id="voice-close-button" class="close-button">&times;</button>
          <div id="voice-outer" class="outer">
            <div class="inner-container">
              <div id="voice-button-container" class="button-container">
                <!-- The audio level animation. -->
                <span id="voice-level" class="level"></span>
                <!-- The microphone button. -->
                <span id="voice-button" class="button">
                  <!-- The microphone icon (in CSS). -->
                  <div class="microphone">
                    <span class="receiver"></span>
                    <div class="wrapper">
                      <span class="stem"></span>
                      <span class="shell"></span>
                    </div>
                  </div>
                </span>
              </div>
              <div id="text-container" aria-live="polite">
                <!-- Low confidence text underneath high confidence text. -->
                <span id="voice-text-i" class="voice-text"></span>
                <!-- High confidence text on top of low confidence text. -->
                <span id="voice-text-f" class="voice-text"></span>
              </div>
            </div>
          </div>
        </div>
      </dialog>
    '''
            text2 = '''
    QTextCharFormat multiLineCommentFormat;
    multiLineCommentFormat.setForeground(Qt::red);
    
    QRegularExpression startExpression("/\\*");
    QRegularExpression endExpression("\\*/");
    
    setCurrentBlockState(0);
    
    int startIndex = 0;
    if (previousBlockState() != 1)
        startIndex = text.indexOf(startExpression);
    
    while (startIndex >= 0) {
       QRegularExpressionMatch endMatch;
       int endIndex = text.indexOf(endExpression, startIndex, &endMatch);
       int commentLength;
       if (endIndex == -1) {
           setCurrentBlockState(1);
           commentLength = text.length() - startIndex;
       } else {
           commentLength = endIndex - startIndex
                           + endMatch.capturedLength();
       }
       setFormat(startIndex, commentLength, multiLineCommentFormat);
       startIndex = text.indexOf(startExpression,
                                 startIndex + commentLength);
    }
            '''
    
            editor.setPlainText(text2)
            editor.resize(400, 250)
            editor.show()
    
            sys.exit(app.exec_())
    
    
        run_test()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
