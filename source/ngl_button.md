---
title: ngl_button
date: 2020-05-07
---
Example Python program ngl_button.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtCore import pyqtSlot, pyqtProperty, QRect, QSize, QPoint, Qt
* from PyQt5.QtGui import QPainter, QColor, QPen, QFont, QFontMetricsF, QImage, QIcon
* from PyQt5.QtWidgets import QWidget
* from qstyle_parser import QStyleParser
* import sys
* from PyQt5.QtWidgets import QApplication

## Classes

* class NGL_Button(QWidget):

## Methods

* def __init__(self, parent=None):
* def paintEvent(self, event):
* def _drawICO(self, painter):
* def _drawText(self, painter, color, flags = Qt.AlignCenter):
* def getColors(self):
* def sizeHint(self):
* def size_update(self):
* def getRect(self):
* def setRect(self, rect):
* def getFont(self):
* def setFont(self, font):
* def getText(self):
* def setText(self, text):
* def getTextSX(self):
* def setTextSX(self, sx):
* def getTextSY(self):
* def setTextSY(self, sy):
* def getGradient(self):
* def setGradient(self, gradient):
* def getICO(self):
* def setICO(self, icon):
* def getType(self):
* def setType(self, ntype):

## Code

Example Python PyQt program :

    #!/usr/bin/env python
    
    from PyQt5.QtCore import pyqtSlot, pyqtProperty, QRect, QSize, QPoint, Qt
    from PyQt5.QtGui import QPainter, QColor, QPen, QFont, QFontMetricsF, QImage, QIcon
    from PyQt5.QtWidgets import QWidget
    from qstyle_parser import QStyleParser
    
    
    class NGL_Button(QWidget):
        """NGL_Button(QWidget)
        Provides a embedded NGL library button widget.
    
        NGL_Button types:
            NGL_Button.text = 'text'
                simple text button with transparent background
            
            NGL_Button.fill = 'fill'
                filled button with or without gradient background
    
            NGL_Button.ico = 'ico'
                only icon button
    
            NGL_Button.ico_text = 'ico_text'  
                icon and text button type
        """
    
        text = 'text'
        fill = 'fill'
        ico = 'ico'
        ico_text = 'ico_text'  
          
    
        def __init__(self, parent=None):
    
            super(NGL_Button, self).__init__(parent)
    
            self.setAutoFillBackground(False)
            self._rect = QRect(0, 0, 70, 45)
            self._gradient = True
            self._font = QFont()
            self._text = self.__class__.__name__
            self._sx = 0
            self._sy = 0        
            self.__ico = QIcon()
            # self._type = self.ico_text
            self.setType(self.fill)
    
            self.setStyleSheet('background-color: rgb(168, 0, 0);\ncolor: rgb(255, 255, 255);')
            self.size_update()
    
        def paintEvent(self, event):
            p = QPainter()        
            p.begin(self)
            
            backcolor, text_color = self.getColors()
    
            if self._type == self.fill:                        
                if self._gradient:
                    pen = QPen(backcolor)
                    
                    for y in range( self._rect.height() ):
                        pen.setColor( backcolor.lighter(100 + (y*2)) )
                        
                        p.setPen( pen )                    
                        x1 = self._rect.x()
                        x2 = x1 + self._rect.width()                    
                        p.drawLine( x1, y, x2, y )                   
                else:
                    p.fillRect(self._rect, backcolor )
    
                self._drawText(p, text_color)
            
            elif self._type == self.ico:
                self._drawICO(p)
    
            elif self._type == self.ico_text:
                self._drawICO(p)
                self._drawText(p, text_color, Qt.AlignHCenter | Qt.AlignBottom)
    
            else:
                self._drawText(p, text_color)
            
            p.end()
    
        def _drawICO(self, painter):
            img = QImage(self.__ico.pixmap(self._rect.width(), self._rect.height()))
            _rect = QRect( self._rect.x(), self._rect.y(), self._rect.width(), self._rect.height() )
            self.__ico.paint( painter, _rect, Qt.AlignHCenter | Qt.AlignTop)         
    
        def _drawText(self, painter, color, flags = Qt.AlignCenter):
            painter.setFont(self._font)
            painter.setPen(color)
            
            rect = QRect( self._rect.x(),
                          self._rect.y(),
                          self._rect.width() + self._sx,
                          self._rect.height() - self._sy )
    
            painter.drawText(rect, flags , self._text)
        
        def getColors(self):
            style = self.styleSheet()
    
            backcolor = QStyleParser.getColor( style, 'background-color: rgb' )            
            if backcolor == None:
                self.setStyleSheet( style + '\nbackground-color: rgb(168, 0, 0);')
                backcolor = QColor(168, 0, 0)
    
            color = QStyleParser.getColor( style, 'color: rgb' )
            if color == None:
                self.setStyleSheet( style + '\ncolor: rgb(0, 0, 0);')
                color = Qt.black
    
            return (backcolor, color)
    
        def sizeHint(self):
            """ return sizeHint """
            return QSize(32, 32)
    
        def size_update(self):
            self.setMinimumSize( self._rect.width()+1, self._rect.height()+1 )
            self.setMaximumSize( self._rect.width()+1, self._rect.height()+1 )
            self.update()
    
        
        # Provide getter and setter methods for the property.
    
        def getRect(self):
            return self._rect
    
        @pyqtSlot(QRect)
        def setRect(self, rect):
            self._rect = rect
            self.size_update()
    
        rect = pyqtProperty(QRect, getRect, setRect)
        
        
        # Provide getter and setter methods for the property.
    
        def getFont(self):
            return self._font
    
        @pyqtSlot(QFont)
        def setFont(self, font):
            self._font = font
            self.update()
    
        font = pyqtProperty(QFont, getFont, setFont)
    
        
        # Provide getter and setter methods for the property.
    
        def getText(self):
            return self._text
    
        @pyqtSlot(str)
        def setText(self, text):
            self._text = text
            self.update()
    
        text = pyqtProperty(str, getText, setText)
    
        
        # Provide getter and setter methods for the property.
    
        def getTextSX(self):
            return self._sx
    
        @pyqtSlot(int)
        def setTextSX(self, sx):
            self._sx = sx
            self.update()
    
        text_sx = pyqtProperty(int, getTextSX, setTextSX)
    
    
        # Provide getter and setter methods for the property.
    
        def getTextSY(self):
            return self._sy
    
        @pyqtSlot(int)
        def setTextSY(self, sy):
            self._sy = sy
            self.update()
    
        text_sy = pyqtProperty(int, getTextSY, setTextSY)
    
    
        # Provide getter and setter methods for the property.
    
        def getGradient(self):
            return self._gradient
    
        @pyqtSlot(bool)
        def setGradient(self, gradient):
            self._gradient = gradient
            self.update()
    
        gradient = pyqtProperty(bool, getGradient, setGradient)
    
        # Provide getter and setter methods for the property.
    
        def getICO(self):
            return self.__ico
    
        @pyqtSlot(QIcon)
        def setICO(self, icon):
            self.__ico = icon        
            self.update()
    
        icon = pyqtProperty(QIcon, getICO, setICO)
    
        # Provide getter and setter methods for the property.
    
        def getType(self):
            return self._type
    
        @pyqtSlot(str)
        def setType(self, ntype):        
            self._type = ntype        
            self.update()
        
        button_type = pyqtProperty(str, getType, setType)
    
        
    
    if __name__ == "__main__":
    
        import sys
        from PyQt5.QtWidgets import QApplication
    
        app = QApplication(sys.argv)
        widget = NGL_Button()   
        widget.show()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
