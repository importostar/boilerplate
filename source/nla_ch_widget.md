---
title: nla_ch_widget
date: 2020-05-07
---
Example Python program nla_ch_widget.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtCore import ( QSize, pyqtSlot, QPointF, Qt, pyqtProperty,
* from PyQt5.QtWidgets import ( QFrame, QWidget, QPushButton, QLineEdit, QLayout,
* from PyQt5.QtGui import ( QFont, QIcon, QLinearGradient, QColor, QPainter,
* from nla_ch_widget import NLA_CH_Widget
*   import sys
*   from PyQt5.QtWidgets import QApplication

## Classes

* class NLA_CH_FrameWidget(QWidget):
* class NLA_CH_Frame(QFrame):

## Methods

*   def __init__(self, parent=None):
*   def channels(self):
*   def channels(self, val):
*   def __init__(self, parent=None):
*   def _set_widget_index(self, widget):
*   def _set_widget_def_index(self, widget):
*   def sort_widgets(self, **kwargv):
*   def add_widget(self, widget):
*   def add_widgets(self, list):
*   def remove_widget(self, widget):
*   def remove_all_widgets(self):
*   def get_indexPosition(self, widget, pos):
*   def mousePressEvent(self, event):
*   def dragEnterEvent(self, event):
*   def dropEvent(self, event):

## Code

Example Python PyQt program :

    # python 3
    
    from PyQt5.QtCore import ( QSize, pyqtSlot, QPointF, Qt, pyqtProperty,
                               QByteArray, QDataStream, QIODevice, QMimeData,
                               QPoint )
    from PyQt5.QtWidgets import ( QFrame, QWidget, QPushButton, QLineEdit, QLayout,
                                  QHBoxLayout, QVBoxLayout, QGridLayout, QSizePolicy,
                                  QStyleFactory, QLabel, QListView, QListWidget, QListWidgetItem )
    from PyQt5.QtGui import ( QFont, QIcon, QLinearGradient, QColor, QPainter,
                              QPen, QFontMetrics, QPixmap, QDrag )
    from nla_ch_widget import NLA_CH_Widget
    
    
    
    class NLA_CH_FrameWidget(QWidget):
      """docstring for NLA_CH_FrameWidget"""
      def __init__(self, parent=None):
        super(NLA_CH_FrameWidget, self).__init__(parent)
    
        sizePolicy1 = QSizePolicy(QSizePolicy.Preferred, QSizePolicy.Fixed)
        font1 = QFont("MS Shell Dlg 2", 9)
        font1.setBold(True)
    
        lbl_title = QLabel('Logic Channels:')
        lbl_title.setSizePolicy(sizePolicy1)
        lbl_title.setMinimumSize(QSize(0, 20))
        lbl_title.setMaximumSize(QSize(16777215, 20))
        lbl_title.setFont(font1)
        lbl_title.setAlignment(Qt.AlignCenter)
    
        lbl_info = QLabel('Neil LA alfa 0.2')
        lbl_info.setSizePolicy(sizePolicy1)
        lbl_info.setMinimumSize(QSize(0, 20))
        lbl_info.setMaximumSize(QSize(16777215, 20))
        lbl_info.setFont(font1)
        lbl_info.setAlignment(Qt.AlignCenter)
    
        self.ch_frame = NLA_CH_Frame(self)
    
        self.vLayout = QVBoxLayout(self)
        self.vLayout.setSpacing(0)
        self.vLayout.setContentsMargins(0, 0, 0, 0)
    
        self.vLayout.addWidget(lbl_title)
        self.vLayout.addWidget(self.ch_frame)
        self.vLayout.addWidget(lbl_info)
    
      @pyqtProperty(int)
      def channels(self):
          return len(self.ch_frame.widgets)
    
      @channels.setter
      def channels(self, val):
          self.ch_frame.remove_all_widgets()
          self.ch_frame.add_widgets([ NLA_CH_Widget(name="channel %s" % i) for i in range(val) ])
    
    
    
    class NLA_CH_Frame(QFrame):
      """docstring for NLA_CH_Frame"""
    
      def __init__(self, parent=None):
          super(NLA_CH_Frame, self).__init__(parent)
    
          self.widgets = []
    
          self.channelsVLayout = QVBoxLayout(self)
          self.channelsVLayout.setSpacing(0)
    
          self.setFrameStyle(QFrame.Sunken | QFrame.StyledPanel)
          self.setAcceptDrops(True)
    
      def _set_widget_index(self, widget):
          if widget.index == None:
            if len(self.widgets):
                widget.index = max([w.index for w in self.widgets]) + 1
            else:
                widget.index = 0
    
      def _set_widget_def_index(self, widget):
          if widget.def_index == None:
            if len(self.widgets):
                widget.def_index = max([w.def_index for w in self.widgets]) + 1
            else:
                widget.def_index = 0
    
      def sort_widgets(self, **kwargv):
          cplist = []
          cplist[:] = self.widgets
    
          self.remove_all_widgets()
    
          list = [i for i in cplist if i != None]
          list = sorted(list, key=lambda obj: obj.index)
    
          indx_reset = kwargv.get('hard', False)
          for widget in list:
              if indx_reset:
                widget.index = None
              self._set_widget_index(widget)
              self.widgets.append(widget)
              self.channelsVLayout.addWidget(widget)
    
      def add_widget(self, widget):
          self._set_widget_def_index(widget)
          self._set_widget_index(widget)
    
          self.widgets.append(widget)
          self.channelsVLayout.addWidget(widget)
    
          self.sort_widgets()
    
      def add_widgets(self, list):
          for item in list:
              self.add_widget(item)
          self.sort_widgets()
          self.update()
    
      def remove_widget(self, widget):
          if widget in self.widgets:
              self.widgets.remove(widget)
    
          widget.setParent(None)
          widget = None
          self.sort_widgets()
    
      def remove_all_widgets(self):
          for w in self.widgets:
            w.setParent(None)
            w = None
          self.widgets = []
    
      def get_indexPosition(self, widget, pos):
          height = widget.size().height()
          return pos.y() // height
    
      def mousePressEvent(self, event):
          child = self.childAt(event.pos())
          if not child or child not in self.widgets:
              return
    
          self.drop_widget = child
          self.drop_widget.selected = True
    
          itemData = QByteArray()
          mimeData = QMimeData()
          mimeData.setData('application/x-dnditemdata', itemData)
    
          drag = QDrag(self)
          drag.setMimeData(mimeData)
          drag.setPixmap(child.pixmap)
          drag.setHotSpot(event.pos() - child.pos())
    
          st = drag.exec_(Qt.CopyAction | Qt.MoveAction, Qt.CopyAction)
          if st == Qt.IgnoreAction:
              self.remove_widget(self.drop_widget)
              self.drop_widget._def_index = None
              self.drop_widget.index = None
              self.add_widget(self.drop_widget)
    
          self.drop_widget.selected = False
          self.sort_widgets(hard=True)
    
      def dragEnterEvent(self, event):
          if event.mimeData().hasFormat('application/x-dnditemdata'):
              if event.source() == self:
                  event.setDropAction(Qt.MoveAction)
    
                  pos_index = self.get_indexPosition(self.drop_widget, event.pos())
    
                  if self.drop_widget.index != pos_index:
                      self.remove_widget(self.drop_widget)
                      self.drop_widget.index = pos_index-1
                      self.add_widget(self.drop_widget)
                      self.sort_widgets(hard=True)
    
                  event.accept()
              else:
                  event.acceptProposedAction()
          else:
              event.ignore()
    
      dragMoveEvent = dragEnterEvent
    
      def dropEvent(self, event):
          if event.mimeData().hasFormat('application/x-dnditemdata'):
    
              if event.source() == self:
                  event.setDropAction(Qt.MoveAction)
                  event.accept()
              else:
                  event.acceptProposedAction()
          else:
              event.ignore()
    
    
    
    # if start as app
    if __name__ == '__main__':
    
      import sys
      from PyQt5.QtWidgets import QApplication
    
      app = QApplication(sys.argv)
      QApplication.setStyle(QStyleFactory.create('Fusion'))
    
      qwidget = NLA_CH_FrameWidget()
      qwidget.channels = 4
      qwidget.show()
    
      sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
