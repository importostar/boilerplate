---
title: range_slider
date: 2020-05-07
---
Example Python program range_slider.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from enum import auto, Flag
* from PyQt5 import QtWidgets
* from PyQt5 import QtGui, QtCore
* from PyQt5.QtCore import QRectF
* from PyQt5.QtGui import QPainter, QPen
* from PyQt5.QtWidgets import QApplication

## Classes

* Verbatim translation of the RangeSlider class from:
* class RangeSlider(QtWidgets.QWidget):
* class Option(Flag):

## Methods

* def __init__(self, parent=None):
* def paintEvent(self, aEvent: QtGui.QPaintEvent) -> None:
* def firstHandleRect(self) -> QtCore.QRectF:
* def secondHandleRect(self) -> QtCore.QRectF:
* def handleRect(self, aValue: float) -> QtCore.QRectF:
* def mousePressEvent(self, aEvent: QtGui.QMouseEvent) -> None:
* def mouseMoveEvent(self, aEvent: QtGui.QMouseEvent):
* def mouseReleaseEvent(self, aEvent: QtGui.QMouseEvent):
* def changeEvent(self, aEvent: QtCore.QEvent):
* def minimumSizeHint(self) -> QtCore.QSize:
* def GetMinimum(self) -> int:
* def SetMinimum(self, aMinimum: int):
* def GetMaximum(self) -> int:
* def SetMaximum(self, aMaximum: int):
* def GetLowerValue(self) -> int:
* def SetLowerValue(self, aLowerValue: int):
* def GetUpperValue(self) -> int:
* def SetUpperValue(self, aUpperValue: int):
* def setLowerValue(self, aLowerValue: int):
* def setUpperValue(self, aUpperValue: int):
* def setMinimum(self, aMinimum: int):
* def setMaximum(self, aMaximum: int):
* def validLength(self) -> int:
* def SetRange(self, aMinimum: int, aMaximum: int):
* def OnLower(x):
* def OnUpper(x):
* def OnRange(x, y):

## Code

Example Python PyQt program :

    """
    Verbatim translation of the RangeSlider class from:
    
    https://github.com/ThisIsClark/Qt-RangeSlider/tree/b3e381fd383aa5b02e78caff9a42fc5f4aab63e6
    
    This is a verbatim translation, without any improvements that could be
    made to the code, such as using max()/min() in a few places, interval comparisons
    (`0 < x < 10` instead of `x > 0 and x < 10`), etc.
    
    The intent is to keep it as close as the original as possible in case we want
    to port bugs upstream or downstream.
    """
    from enum import auto, Flag
    
    from PyQt5 import QtWidgets
    from PyQt5 import QtGui, QtCore
    from PyQt5.QtCore import QRectF
    from PyQt5.QtGui import QPainter, QPen
    from PyQt5.QtWidgets import QApplication
    
    scHandleSideLength = 11
    scSliderBarHeight = 5
    scLeftRightMargin = 1
    
    
    class RangeSlider(QtWidgets.QWidget):
        """
        Implements a Range slider: a control which defines a (min, max) integer interval,
        being displayed as two slider handles for each end.
        """
    
        lowerValueChanged = QtCore.pyqtSignal(int)
        upperValueChanged = QtCore.pyqtSignal(int)
        rangeChanged = QtCore.pyqtSignal(int, int)
    
        class Option(Flag):
            NoHandle = auto()
            LeftHandle = auto()
            RightHandle = auto()
            DoubleHandles = LeftHandle | RightHandle
    
        def __init__(self, parent=None):
            super().__init__(parent)
    
            self.mMinimum = 0
            self.mMaximum = 100
            self.mLowerValue = 0
            self.mUpperValue = 100
            self.mFirstHandlePressed = False
            self.mSecondHandlePressed = False
            self.mInterval = self.mMaximum - self.mMinimum
            self.mBackgroudColorEnabled = QtGui.QColor(0x1E, 0x90, 0xFF)
            self.mBackgroudColorDisabled = QtCore.Qt.darkGray
            self.mBackgroudColor = self.mBackgroudColorEnabled
            self.orientation = QtCore.Qt.Horizontal
            self.type = self.Option.DoubleHandles
    
            self.setMouseTracking(True)
    
        def paintEvent(self, aEvent: QtGui.QPaintEvent) -> None:
            painter = QtGui.QPainter(self)
    
            # Background
            if self.orientation == QtCore.Qt.Horizontal:
                backgroundRect = QRectF(scLeftRightMargin, (self.height() - scSliderBarHeight) / 2, self.width() - scLeftRightMargin * 2, scSliderBarHeight)
            else:
                backgroundRect = QRectF((self.width() - scSliderBarHeight) / 2, scLeftRightMargin, scSliderBarHeight, self.height() - scLeftRightMargin*2)
    
            pen = QPen(QtCore.Qt.gray, 0.8)
            painter.setPen(pen)
            painter.setRenderHint(QtGui.QPainter.Qt4CompatiblePainting)
            backgroundBrush = QtGui.QBrush(QtGui.QColor(0xD0, 0xD0, 0xD0))
            painter.setBrush(backgroundBrush)
            painter.drawRoundedRect(backgroundRect, 1, 1)
    
            # First value handle rect
            pen.setColor(QtCore.Qt.darkGray)
            pen.setWidth(0.5)
            painter.setPen(pen)
            painter.setRenderHint(QtGui.QPainter.Antialiasing)
            handleBrush = QtGui.QBrush(QtGui.QColor(0xFA, 0xFA, 0xFA))
            painter.setBrush(handleBrush)
            leftHandleRect = self.firstHandleRect()
            if self.Option.LeftHandle in self.type:
                painter.drawRoundedRect(leftHandleRect, 2, 2)
    
            # Second value handle rect
            rightHandleRect = self.secondHandleRect()
            if self.Option.RightHandle in self.type:
                painter.drawRoundedRect(rightHandleRect, 2, 2)
    
            # Handles
            painter.setRenderHint(QtGui.QPainter.Antialiasing, False)
            selectedRect = QtCore.QRectF(backgroundRect)
            if self.orientation == QtCore.Qt.Horizontal:
                selectedRect.setLeft((leftHandleRect.right() if self.Option.LeftHandle in self.type else leftHandleRect.left()) + 0.5)
                selectedRect.setRight((rightHandleRect.left() if self.Option.RightHandle in self.type else rightHandleRect.right()) - 0.5)
            else:
                selectedRect.setTop((leftHandleRect.bottom() if self.Option.LeftHandle in self.type else leftHandleRect.top()) + 0.5)
                selectedRect.setBottom((rightHandleRect.top() if self.Option.RightHandle in self.type else rightHandleRect.bottom()) - 0.5)
            
            selectedBrush = QtGui.QBrush(self.mBackgroudColor)
            painter.setBrush(selectedBrush)
            painter.drawRect(selectedRect)
    
        def firstHandleRect(self) -> QtCore.QRectF:
            percentage = (self.mLowerValue - self.mMinimum) * 1.0 / self.mInterval
            return self.handleRect(percentage * self.validLength() + scLeftRightMargin)
    
        def secondHandleRect(self) -> QtCore.QRectF:
            percentage = (self.mUpperValue - self.mMinimum) * 1.0 / self.mInterval
            return self.handleRect(percentage * self.validLength() + scLeftRightMargin + (
                scHandleSideLength if self.Option.LeftHandle in self.type else 0))
    
        def handleRect(self, aValue: float) -> QtCore.QRectF:
            aValue = int(aValue)
            if self.orientation == QtCore.Qt.Horizontal:
                return QtCore.QRect(aValue, (self.height() - scHandleSideLength) // 2,
                                    scHandleSideLength, scHandleSideLength)
            else:
                return QtCore.QRect((self.width() - scHandleSideLength) // 2, aValue,
                                    scHandleSideLength, scHandleSideLength)
    
        def mousePressEvent(self, aEvent: QtGui.QMouseEvent) -> None:
            if aEvent.buttons() & QtCore.Qt.LeftButton:
                posCheck = aEvent.pos().y() if self.orientation == QtCore.Qt.Horizontal else aEvent.pos().x()
                posMax = self.height() if self.orientation == QtCore.Qt.Horizontal else self.width()
                posValue = aEvent.pos().x() if self.orientation == QtCore.Qt.Horizontal else aEvent.pos().y()
                firstHandleRectPosValue = self.firstHandleRect().x() if self.orientation == QtCore.Qt.Horizontal else self.firstHandleRect().y()
                secondHandleRectPosValue = self.secondHandleRect().x() if self.orientation == QtCore.Qt.Horizontal else self.secondHandleRect().y()
    
                self.mSecondHandlePressed = self.secondHandleRect().contains(aEvent.pos())
                self.mFirstHandlePressed = not self.mSecondHandlePressed and self.firstHandleRect().contains(aEvent.pos())
    
                if self.mFirstHandlePressed:
                    self.mDelta = posValue - (firstHandleRectPosValue + scHandleSideLength / 2)
    
                elif self.mSecondHandlePressed:
                    self.mDelta = posValue - (secondHandleRectPosValue + scHandleSideLength / 2)
    
                elif posCheck >= 2 and posCheck <= posMax - 2:
                    step = 1 if self.mInterval // 10 < 1 else self.mInterval // 10
                    if posValue < firstHandleRectPosValue:
                        self.setLowerValue(self.mLowerValue - step)
                    elif posValue > secondHandleRectPosValue + scHandleSideLength:
                        self.setUpperValue(self.mUpperValue + step)
                    elif ((posValue > firstHandleRectPosValue + scHandleSideLength) or self.Option.LeftHandle not in self.type
                            and ((posValue < secondHandleRectPosValue) or self.Option.RightHandle not in self.type)):
                        if self.Option.DoubleHandles in self.type:
                            if(posValue - (firstHandleRectPosValue + scHandleSideLength) <
                                    (secondHandleRectPosValue - (firstHandleRectPosValue + scHandleSideLength)) // 2):
                                self.setLowerValue(self.mLowerValue + step if (self.mLowerValue + step < self.mUpperValue) else self.mUpperValue)
                            else:
                                self.setUpperValue(self.mUpperValue - step if (self.mUpperValue - step > self.mLowerValue) else self.mLowerValue)
                        elif self.Option.LeftHandle in self.type:
                            self.setLowerValue(self.mLowerValue + step if (self.mLowerValue + step < self.mUpperValue) else self.mUpperValue)
                        elif self.Option.RightHandle in self.type:
                            self.setUpperValue(self.mUpperValue - step if (self.mUpperValue - step > self.mLowerValue) else self.mLowerValue)
    
        def mouseMoveEvent(self, aEvent: QtGui.QMouseEvent):
            if aEvent.buttons() & QtCore.Qt.LeftButton:
    
                posValue = aEvent.pos().x() if self.orientation == QtCore.Qt.Horizontal else aEvent.pos().y()
                firstHandleRectPosValue = self.firstHandleRect().x() if self.orientation == QtCore.Qt.Horizontal else self.firstHandleRect().y()
                secondHandleRectPosValue = self.secondHandleRect().x() if self.orientation == QtCore.Qt.Horizontal else self.secondHandleRect().y()
    
                if self.mFirstHandlePressed and self.Option.LeftHandle in self.type:
    
                    if posValue - self.mDelta + scHandleSideLength / 2 <= secondHandleRectPosValue:
                        self.setLowerValue((posValue - self.mDelta - scLeftRightMargin - scHandleSideLength / 2) * 1.0 / self.validLength() * self.mInterval + self.mMinimum)
                    else:
                        self.setLowerValue(self.mUpperValue)
                elif(self.mSecondHandlePressed and self.Option.RightHandle in self.type):
                    if(firstHandleRectPosValue + scHandleSideLength * (1.5 if self.Option.DoubleHandles in self.type else 0.5) <= posValue - self.mDelta):
                        self.setUpperValue((posValue - self.mDelta - scLeftRightMargin - scHandleSideLength / 2 - (scHandleSideLength if self.Option.DoubleHandles in self.type else 0)) * 1.0 / self.validLength() * self.mInterval + self.mMinimum)
                    else:
                        self.setUpperValue(self.mLowerValue)
    
        def mouseReleaseEvent(self, aEvent: QtGui.QMouseEvent):
            self.mFirstHandlePressed = False
            self.mSecondHandlePressed = False
    
        def changeEvent(self, aEvent: QtCore.QEvent):
    
            if aEvent.type() == QtCore.QEvent.EnabledChange:
                if self.isEnabled():
                    self.mBackgroudColor = self.mBackgroudColorEnabled
                else:
                    self.mBackgroudColor = self.mBackgroudColorDisabled
                self.update()
    
        def minimumSizeHint(self) -> QtCore.QSize:
            return QtCore.QSize(scHandleSideLength * 2 + scLeftRightMargin * 2, scHandleSideLength)
    
        def GetMinimum(self) -> int:
            return self.mMinimum
    
        def SetMinimum(self, aMinimum: int):
            self.setMinimum(aMinimum)
    
        def GetMaximum(self) -> int:
            return self.mMaximum
    
        def SetMaximum(self, aMaximum: int):
            self.setMaximum(aMaximum)
            
        def GetLowerValue(self) -> int:
            return int(self.mLowerValue)
    
        def SetLowerValue(self, aLowerValue: int):
            self.setLowerValue(aLowerValue)
    
        def GetUpperValue(self) -> int:
            return int(self.mUpperValue)
    
        def SetUpperValue(self, aUpperValue: int):
            self.setUpperValue(aUpperValue)
    
        def setLowerValue(self, aLowerValue: int):
            if aLowerValue > self.mMaximum:
                aLowerValue = self.mMaximum
    
            if aLowerValue < self.mMinimum:
                aLowerValue = self.mMinimum
    
            self.mLowerValue = aLowerValue
            self.lowerValueChanged.emit(self.mLowerValue)
    
            self.update()
    
        def setUpperValue(self, aUpperValue: int):
            if aUpperValue > self.mMaximum:
                aUpperValue = self.mMaximum
    
            if aUpperValue < self.mMinimum:
                aUpperValue = self.mMinimum
    
            self.mUpperValue = aUpperValue
            self.upperValueChanged.emit(self.mUpperValue)
    
            self.update()
    
        def setMinimum(self, aMinimum: int):
            if aMinimum <= self.mMaximum:
                self.mMinimum = aMinimum
            else:
                oldMax = self.mMaximum
                self.mMinimum = oldMax
                self.mMaximum = aMinimum
            self.mInterval = self.mMaximum - self.mMinimum
            self.update()
    
            self.setLowerValue(self.mMinimum)
            self.setUpperValue(self.mMaximum)
    
            self.rangeChanged.emit(self.mMinimum, self.mMaximum)
    
        def setMaximum(self, aMaximum: int):
            if(aMaximum >= self.mMinimum):
                self.mMaximum = aMaximum
            else:
                oldMin = self.mMinimum
                self.mMaximum = oldMin
                self.mMinimum = aMaximum
    
            self.mInterval = self.mMaximum - self.mMinimum
            self.update()
    
            self.setLowerValue(self.mMinimum)
            self.setUpperValue(self.mMaximum)
    
            self.rangeChanged.emit(self.mMinimum, self.mMaximum)
    
        def validLength(self) -> int:
            len = self.width() if self.orientation == QtCore.Qt.Horizontal else self.height()
            return len - scLeftRightMargin * 2 - scHandleSideLength * (
                2 if self.type.DoubleHandles in self.type else 1)
    
        def SetRange(self, aMinimum: int, aMaximum: int):
            self.setMinimum(aMinimum)
            self.setMaximum(aMaximum)
    
    
    if __name__ == "__main__":
    
        def OnLower(x):
            print(f'Lower: {x}')
    
        def OnUpper(x):
            print(f'OnUpper: {x}')
            
        def OnRange(x, y):
            print(f'Range: {x} {y}')
    
        app = QApplication([])
        slider = RangeSlider(None)
        slider.lowerValueChanged.connect(OnLower)
        slider.upperValueChanged.connect(OnUpper)
        slider.rangeChanged.connect(OnRange)
        slider.SetRange(50, 60)
        slider.show()
        app.exec_()
        
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
