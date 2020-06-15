---
title: CalendarView
date: 2020-05-07
---
Example Python program CalendarView.py
This program creates a PyQt GUI

## Modules

* import typing
* from PyQt5.QtCore import QDate
* from PyQt5.QtCore import Qt, QAbstractTableModel, QItemSelectionModel, QItemSelection, QModelIndex
* from PyQt5.QtGui import QMouseEvent
* from PyQt5.QtWidgets import QTableView, QAbstractItemView
* import sys
* from PyQt5.QtWidgets import QApplication, QTableView

## Classes

* class TableModel(QAbstractTableModel):
* class CalendarView(QTableView):

## Methods

* def __init__(self):
* def headerData(self, section: int, orientation: Qt.Orientation, role: int = ...) -> typing.Any:
* def data(self, index, role):
* def rowCount(self, index):
* def columnCount(self, index):
* def __init__(self):
* def mousePressEvent(self, e: QMouseEvent) -> None:
* def index(self, row, col):
* def currentChanged(self, current: QModelIndex, previous: QModelIndex) -> None:

## Code

Example Python PyQt program :

    import typing
    
    from PyQt5.QtCore import QDate
    from PyQt5.QtCore import Qt, QAbstractTableModel, QItemSelectionModel, QItemSelection, QModelIndex
    from PyQt5.QtGui import QMouseEvent
    from PyQt5.QtWidgets import QTableView, QAbstractItemView
    
    
    class TableModel(QAbstractTableModel):
        def __init__(self):
            super(TableModel, self).__init__()
    
        def headerData(self, section: int, orientation: Qt.Orientation, role: int = ...) -> typing.Any:
            if orientation == Qt.Horizontal and role == Qt.DisplayRole:
                return QDate.longDayName(section + 1)
    
        def data(self, index, role):
            if role == Qt.DisplayRole:
                return index.row() * 7 + index.column() + 1
    
        def rowCount(self, index):
            return 6
    
        def columnCount(self, index):
            return 7
    
    
    class CalendarView(QTableView):
    
        def __init__(self):
            super(CalendarView, self).__init__()
            self.setSelectionMode(QAbstractItemView.NoSelection)
            self._start: typing.Union[QModelIndex, None] = None
    
        def mousePressEvent(self, e: QMouseEvent) -> None:
            self._start = self.indexAt(e.pos())
            self.clearSelection()
            self.selectionModel().select(self._start, QItemSelectionModel.Select)
            super(CalendarView, self).mousePressEvent(e)
    
        def index(self, row, col):
            return self.model().index(row, col)
    
        def currentChanged(self, current: QModelIndex, previous: QModelIndex) -> None:
            if self.state() == QAbstractItemView.DragSelectingState:
                self.clearSelection()
                if current.row() == self._start.row():  # we only have one row, select from start to current
                    selection = QItemSelection(self._start, self.model().index(self._start.row(), current.column()))
                else:  # more than one row selected make the other 2 selections
                    selection = QItemSelection(self._start, current)
                    if current.row() < self._start.row():  # stencil out diagonal
                        right = QItemSelection(current, self.index(self._start.row() - 1, 6))
                        left = QItemSelection(self.index(current.row() + 1, 0), self._start)
                        selection.merge(right, QItemSelectionModel.Select)
                        selection.merge(left, QItemSelectionModel.Select)
                        if current.column() > self._start.column():
                            stencil = QItemSelection(self.index(current.row(), current.column() - 1),
                                                     self.index(current.row(), 0))
                            stencil2 = QItemSelection(self.index(self._start.row(), self._start.column() + 1),
                                                      self.index(self._start.row(), 6))
                            selection.merge(stencil, QItemSelectionModel.Deselect)
                            selection.merge(stencil2, QItemSelectionModel.Deselect)
                    else:
                        right = QItemSelection(self._start, self.index(current.row() - 1, 6))
                        left = QItemSelection(self.index(self._start.row() + 1, 0), current)
                        selection.merge(right, QItemSelectionModel.Select)
                        selection.merge(left, QItemSelectionModel.Select)
                        if current.column() < self._start.column():  # stencil out diagonal
                            stencil = QItemSelection(self.index(self._start.row(), self._start.column() - 1),
                                                     self.index(self._start.row(), 0))
                            stencil2 = QItemSelection(self.index(current.row(), current.column() + 1),
                                                      self.index(current.row(), 6))
                            selection.merge(stencil, QItemSelectionModel.Deselect)
                            selection.merge(stencil2, QItemSelectionModel.Deselect)
                self.selectionModel().select(selection, QItemSelectionModel.Select)
    
    
    if __name__ == '__main__':
        import sys
        from PyQt5.QtWidgets import QApplication, QTableView
    
        app = QApplication(sys.argv)
    
        model = TableModel()
    
        cal = CalendarView()
        cal.setModel(model)
        cal.show()
    
        cal.resize(860, 640)
    
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
