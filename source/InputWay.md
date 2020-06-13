---
title: InputWay
date: 2020-05-07
---
Example Python program InputWay.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from PyQt5.QtWidgets import *
* from PyQt5.QtCore import *
* from PyQt5.QtGui import *
* from underlying import Route

## Classes

* class InputWay(QWidget):

## Methods

* def __init__(self):
* def initUI(self):
* def ButtonWay(self):
* def ButtonSearch(self):
* def ButtonRoute(self):
* def ButtonClose(self):
* def wheelEvent(self, event):
* def mousePressEvent(self, event):
* def mouseReleaseEvent(self, event):
* def mouseMoveEvent(self, event):

## Code

Example Python PyQt program :

    import sys
    from PyQt5.QtWidgets import *
    from PyQt5.QtCore import *
    from PyQt5.QtGui import *
    sys.path.append(r'..')
    from underlying import Route
    class InputWay(QWidget):
        def __init__(self):
            super(InputWay, self).__init__()
            self.initUI()
    
        def initUI(self):
            self.setWindowTitle('输入框设计')
    #        self.setWindowFlags(Qt.FramelessWindowHint)  # 无边框
            self.resize(960, 540)
            self.way = Route.Route()
            self.setCursor(Qt.OpenHandCursor)#setCursor(Qt.ClosedHandCursor)握手鼠标指针
            self.setMinimumSize(1920, 1440)
            #设置背景图片，即地图
            self.map = QPalette()
            self.map.setBrush(self.backgroundRole(), QBrush(QPixmap('../image/map.jpg')))
    #        self.map.setBrush(self.foregroundRole(), QBrush(QPixmap('../image/map.jpg')))
            self.setPalette(self.map)
    
            # 创建一个滚动条
            self.scroll = QScrollArea()
            self.scroll.setWidget(self)
            self.vSb = self.scroll.verticalScrollBar()
            self.hSb = self.scroll.horizontalScrollBar()
            self.scroll.setVerticalScrollBarPolicy(Qt.ScrollBarAlwaysOff)  # 隐藏纵向滚动条
            self.scroll.setHorizontalScrollBarPolicy(Qt.ScrollBarAlwaysOff)
            self.scroll.show()
    
    #        self.layout = QGridLayout(self)
            self.point = QLineEdit(self)
            self.point.setFixedSize(400, 40)#设置输入文本框大小
            self.point.setPlaceholderText('输入景点、车站名称')
            self.point.move(40, 20)
            self.point.show()
    
            self.begin_point = QLineEdit(self)#起点文本输入框
            self.begin_point.setPlaceholderText('输入起点或在图区上选点')
            self.begin_point.setFixedSize(400, 40)
            self.begin_point.move(40, 60)
    
            self.end_point = QLineEdit(self)  # 终点文本输入框
            self.end_point.setPlaceholderText('输入终点或在图区上选点')
            self.end_point.setFixedSize(400, 40)
            self.end_point.move(40, 100)
    
            #关闭按钮
            self.button_close = QPushButton(self)
            self.button_close.setIcon(QIcon(QPixmap('../image/close.jpg')))
            self.button_close.setToolTip('关闭')
            self.button_close.setIconSize(QSize(39, 39))
            self.button_close.setFixedSize(40, 40)
            self.button_close.setCursor(QCursor(Qt.PointingHandCursor))
            self.button_close.clicked.connect(self.ButtonClose)
            self.button_close.move(440, 20)
    
            #搜索路径按钮
            self.button_way = QPushButton(self)
            self.button_way.setIcon(QIcon(QPixmap('../image/way.png')))
            self.button_way.setIconSize(QSize(39, 39))
            self.button_way.setFixedSize(40, 40)
            self.button_way.setToolTip('路线')
            self.button_way.setCursor(QCursor(Qt.PointingHandCursor))
            self.button_way.clicked.connect(self.ButtonWay)
            self.button_way.move(440, 20)
            self.button_way.show()
    
            #查找按钮
            self.button_search = QPushButton(self)
            self.button_search.setIcon(QIcon(QPixmap('../image/search.jpg')))
            self.button_search.setFixedSize(39, 39)
            self.button_search.setIconSize(QSize(40, 40))
            self.button_search.setToolTip('搜索')
            self.button_search.clicked.connect(self.ButtonSearch)
            self.button_search.setCursor(QCursor(Qt.PointingHandCursor))
            self.button_search.move(480, 20)
            self.button_search.show()
    
            self.content = QTextEdit(self)
            self.content.setFixedSize(400, 200)
            self.content.move(40, 60)
    #        Hlayout = QHBoxLayout()#水平布局
    #        Vlayout = QVBoxLayout()#垂直布局
    
    #        self.layout.addWidget(self.point, 0, 1)
    #        self.layout.addWidget(self.button_way, 0, 2)
    #        self.layout.addWidget(self.button_search, 0, 3)
    #        self.layout.setAlignment(Qt.AlignCenter)
    
    #       self.setLayout(self.layout)
        def ButtonWay(self):
            self.button_way.close()
            self.content.close()
            self.point.close()
            self.button_close.show()
            self.begin_point.show()
            self.end_point.show()
            self.point.setText("")
            # 搜索按钮
            self.button_search.clicked.disconnect(self.ButtonSearch)
            self.button_search.clicked.connect(self.ButtonRoute)
    
        #搜索景点相关信息
        def ButtonSearch(self):
            point = self.point.text().replace(' ', '')
            if self.way.IsSpot(point) == 1:
                print(point)
                information = self.way.Attration(point)
                self.content.setPlainText(information)
                self.content.show()
    
            else:
                print("并未找到相关景点")
    
        #查找路径
        def ButtonRoute(self):
            begin = self.begin_point.text()
            end = self.end_point.text()
            begin = begin.replace(' ', '')
            end = end.replace(' ', '')
            print(begin, end)
            Judge_begin = self.way.IsSpot(begin)
            Judge_end = self.way.IsSpot(end)
            if Judge_begin == 0:
                print("起始点输入错误")
    
            if Judge_end == 0:
                print("终点输入错误")
    
            if Judge_begin and Judge_end:
                print(begin, end)
                path_foot = self.way.FootRoute(begin, end)
                path_bus = self.way.BusRoute(begin, end)
                path_time = self.way.TimeRoute(begin, end)
                print(path_foot)
                print(path_bus)
                print(path_time)
    
    
        #关闭路径查找
        def ButtonClose(self):
            self.button_way.show()
            self.point.show()
            self.button_close.close()
            self.begin_point.close()
            self.end_point.close()
            self.begin_point.setText("")
            self.end_point.setText("")
            self.button_search.clicked.disconnect(self.ButtonRoute)
            self.button_search.clicked.connect(self.ButtonSearch)
    
        def wheelEvent(self, event):
            angle = event.angleDelta()
            y = angle.y()
            print(y)
            self.vSb.setValue(self.vSb.value() - y)
    
    #鼠标左键按住事件
        def mousePressEvent(self, event):
            self.setCursor(Qt.ClosedHandCursor)
    
            angle = event.localPos()
            self.x = angle.x()
            self.y = angle.y()
            if event.buttons() == Qt.LeftButton:
                self.x0 = self.hSb.value()
                self.y0 = self.vSb.value()
    
        #释放鼠标响应事件
        def mouseReleaseEvent(self, event):
            self.setCursor(Qt.OpenHandCursor)
    
    #鼠标移动响应事件
        def mouseMoveEvent(self, event):
            print(Qt.LeftButton)
            if Qt.LeftButton:
                angle = event.pos()
                y = angle.y() - self.y
                x = angle.x() - self.x
                self.vSb.setValue(self.y0 - y)
                self.hSb.setValue(self.x0 - x)
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
    #   qssStyle = '''
    #        QPushButton{border-image:url(../image/mouse.jpg);}
    #    '''
        main = InputWay()
    #    main.setStyleSheet(qssStyle)
        main.show()
    
        sys.exit(app.exec_())
    '''        
    self.button_search.setStyleSheet("QPushButton{color:black}"
                                     "QPushButton:hover{color:red}"
                                     "QPushButton{background-color:lightgreen}"
                                     "QPushButton{border:2px}"
                                     "QPushButton{border-radius:10px}"
                                     "QPushButton{padding:2px 4px}")
    '''

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
