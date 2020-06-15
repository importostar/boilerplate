---
title: delegate
date: 2020-05-07
---
Example Python program delegate.py

## Modules

* from PyQt5.QtCore import QModelIndex, QPoint, QSize, Qt
* from PyQt5.QtGui import QTextDocument, QAbstractTextDocumentLayout, QPainter, QLinearGradient, QColor, QPalette
* from PyQt5.QtWidgets import QStyledItemDelegate, QStyle, QStyleOptionViewItem

## Classes

* class HtmlDelegate(QStyledItemDelegate):

## Methods

* def find_colors(option: QStyleOptionViewItem, even_row: bool):
* def __init__(self, parent=None):
* def paint(self, painter: QPainter, option: QStyleOptionViewItem, index: QModelIndex):
* def sizeHint(self, option: QStyleOptionViewItem, index: QModelIndex):

## Code

Example Python PyQt program :

    from PyQt5.QtCore import QModelIndex, QPoint, QSize, Qt
    from PyQt5.QtGui import QTextDocument, QAbstractTextDocumentLayout, QPainter, QLinearGradient, QColor, QPalette
    from PyQt5.QtWidgets import QStyledItemDelegate, QStyle, QStyleOptionViewItem
    
    
    def find_colors(option: QStyleOptionViewItem, even_row: bool):
        if option.state & QStyle.State_Active and option.state & QStyle.State_Selected:
            text_color = option.palette.color(QPalette.Active, QPalette.HighlightedText)
            bg_color = option.palette.color(QPalette.Active, QPalette.Highlight)
        elif option.state & QStyle.State_Selected:
            text_color = option.palette.color(QPalette.Inactive, QPalette.Text)
            bg_color = option.palette.color(QPalette.Inactive, QPalette.Highlight)
        elif even_row and option.state & QStyle.State_Active:
            text_color = option.palette.color(QPalette.Inactive, QPalette.Text)
            bg_color = option.palette.color(QPalette.Active, QPalette.Base)
        elif even_row:
            text_color = option.palette.color(QPalette.Inactive, QPalette.Text)
            bg_color = option.palette.color(QPalette.Inactive, QPalette.Base)
        elif option.state & QStyle.State_Active:
            text_color = option.palette.color(QPalette.Inactive, QPalette.Text)
            bg_color = option.palette.color(QPalette.Active, QPalette.AlternateBase)
        else:
            text_color = option.palette.color(QPalette.Inactive, QPalette.Text)
            bg_color = option.palette.color(QPalette.Inactive, QPalette.AlternateBase)
        return text_color, bg_color
    
    
    class HtmlDelegate(QStyledItemDelegate):
    
        def __init__(self, parent=None):
            super().__init__(parent)
            self.__text_doc = QTextDocument()
            self.__text_doc.setDocumentMargin(0.0)
    
        def paint(self, painter: QPainter, option: QStyleOptionViewItem, index: QModelIndex):
            new_option = QStyleOptionViewItem(option)
            self.initStyleOption(new_option, index)
    
            self.__text_doc.setHtml(new_option.text)
            new_option.text = ""
    
            style = new_option.widget.style()
            style.drawControl(QStyle.CE_ItemViewItem, new_option, painter, new_option.widget)
    
            text_rect = style.subElementRect(QStyle.SE_ItemViewItemText, new_option, new_option.widget)
            pc = QAbstractTextDocumentLayout.PaintContext()
    
            # Colors
            tc, bg = find_colors(new_option, index.row() % 2 == 0)
            pc.palette.setColor(QPalette.Text, tc)
    
            # Points
            text_point = QPoint(text_rect.topLeft().x() + 2,
                                text_rect.topLeft().y() + round(
                                    0.5 * (option.rect.height() - self.__text_doc.size().height())))
            grad_point = QPoint(text_rect.topRight().x() - 43, option.rect.topRight().y())
    
            # Gradient
            gradient = QLinearGradient(grad_point.x(), option.rect.height(), grad_point.x() + 35, option.rect.height())
            gradient.setColorAt(0, QColor(Qt.transparent))
            gradient.setColorAt(1, bg)
    
            # Paint action
            painter.save()
            painter.translate(text_point)
            self.__text_doc.documentLayout().draw(painter, pc)
            painter.translate(-text_point)
            painter.fillRect(option.rect, gradient)
            painter.restore()
    
        def sizeHint(self, option: QStyleOptionViewItem, index: QModelIndex):
            return QSize(int(self.__text_doc.idealWidth()), int(self.__text_doc.size().height()))
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
