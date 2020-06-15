---
title: mian_page008
date: 2020-05-07
---
Example Python program mian_page008.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5.QtWidgets import *
* from PyQt5.QtGui import *
* from PyQt5.QtCore import Qt
* import math
* from database_search.Sunny_Database import Database

## Classes

* class PageController(QWidget):
* class BasicTableView(QTableView):
* class BasicTreeWidget(QTreeWidget):
* class Data_Mainwindow(QMainWindow):

## Methods

* def __init__(self, page: int):
* def _init_ui(self):
* def __init__(self):
* def _init_ui(self):
* def show_data(self, rows: list, column_names: list, is_trim=False):
* def __init__(self, parent=None):
* def _init_ui(self):
* def set_tree_children(self, da_table, test_table):
* def __init__(self):
* def set_menu(self):
* def _init_ui(self):
* def pre_next_page(self, offset):
* def onSkipPage(self):
* def _search_table(self, table_name: str, skip_page=1):
* def onTreedoubleClicked(self, index):
* def find_module_info(self):
* def set_font(self):
* def set_font_color(self):
* def quit_trigger(self):

## Code

Example Python PyQt program :

    '''
    1、分页显示数据
    2、重新查询数据，再显示数据
    '''
    '''
    1、左边树控件实现数据库的DA、测试表的浏览和查找
    2、右侧tableview控件实现数据库数据的展示
        1）下方数据的分页显示
        2）线程优化：UI线程不卡死，后台把数据扔到前端渲染
        3）NG和OK数据颜色标明，字体等的显示
        4）缓存增加数据保存的速度
    3、菜单栏增加数据保存和查询
    4、后期增加数据可视化等的优化
    '''
    import sys
    from PyQt5.QtWidgets import *
    from PyQt5.QtGui import *
    from PyQt5.QtCore import Qt
    import math
    
    from database_search.Sunny_Database import Database
    
    '''
    1、树控件点击由树控件本身，挪到了主界面里进行相应的响应
    2、表增加NG和OK数据颜色显示，后期增加用户颜色喜好设置
    3、目前设置合理大小，后期优化窗口本身的鼠标左右挪动实现
    4、优化每次双击表进入，TableView不刷新现象
    5、大量数据，需要后台线程优化,但线程优化效率不佳
    6、测试数据由于ID是计数的，可以进行分页显示；而DA表没有ID技术，所以默认显示前500吧
    
    
    '''
    
    
    
    class PageController(QWidget):
        def __init__(self, page: int):
            super().__init__()
            self._page = page
            self._init_ui()
    
        def _init_ui(self):
            control_layout = QHBoxLayout()
            self.prePage = QPushButton("<上一页")
            self.curPage = QLabel("1")
            self.nextPage = QPushButton("下一页>")
    
            self.totalPage = QLabel("共" + str(self._page) + "页")
            skipLable_0 = QLabel("跳到")
            self.skipPage = QLineEdit()
            self.skipPage.setValidator(QIntValidator())  # 设置只能输入int类型的数据
            skipLabel_1 = QLabel("页")
            self.confirmSkip = QPushButton("确定")
    
            control_layout.addStretch(1)
            control_layout.addWidget(self.prePage)
            control_layout.addWidget(self.curPage)
            control_layout.addWidget(self.nextPage)
            control_layout.addWidget(self.totalPage)
            control_layout.addWidget(skipLable_0)
            control_layout.addWidget(self.skipPage)
            control_layout.addWidget(skipLabel_1)
            control_layout.addWidget(self.confirmSkip)
            control_layout.addStretch(1)
    
            self.setLayout(control_layout)
    
    
    class BasicTableView(QTableView):
        def __init__(self):
            super().__init__()
            ##必须放在初始化时，赋值及定义，放在show_data方法中有问题，不能动态的改变属性，
            # 而QStandardItemModel的clear会直接动态的删除Model的数据，view也就没有了
            self.model = QStandardItemModel()
            self._init_ui()
    
        def _init_ui(self):
            ##QTableView控件的设置
            self.tableview = QTableView()
            # 关联QTableView和Model
            self.tableview.setModel(self.model)
    
            self.tableview.horizontalHeader().setStretchLastSection(True)
            self.tableview.horizontalHeader().setSectionResizeMode(QHeaderView.Interactive)
            self.tableview.setEditTriggers(QAbstractItemView.NoEditTriggers)  # 不可编辑
            self.tableview.setSelectionMode(QAbstractItemView.SingleSelection)  # 设置只能选中一行
            self.tableview.setSelectionBehavior(QAbstractItemView.SelectRows)  # 设置只有行选中
    
            style_sheet = """
                        QTableView {
                            border: none;
                            background-color:rgb(255,255,255)
                        }
                        """
            self.tableview.setStyleSheet(style_sheet)
    
            # 样式
            layout = QVBoxLayout()
            layout.addWidget(self.tableview)
    
            self.setLayout(layout)
    
        def show_data(self, rows: list, column_names: list, is_trim=False):
            self.model.setRowCount(len(rows))
            self.model.setColumnCount(len(column_names))
            self.model.setHorizontalHeaderLabels(column_names)
    
            # 添加数据
            for num0, item0 in enumerate(rows):
                if is_trim:
                    item0 = item0[:-1]
                for num1, item1 in enumerate(item0):
                    qstd_item = QStandardItem(str(item1))
                    self.model.setItem(num0, num1, qstd_item)
                    if 'NG' in item0:
                        # qstd_item.setBackground(QBrush(QColor(255,255,0)))
                        qstd_item.setBackground(QBrush(QColor(255, 102, 102)))
                    else:
                        qstd_item.setBackground(QBrush(QColor(153, 204, 102)))
    
    
    class BasicTreeWidget(QTreeWidget):
        def __init__(self, parent=None):
            super(BasicTreeWidget, self).__init__(parent)
    
            self._init_ui()
    
        def _init_ui(self):
            self.setColumnCount(1)
            self.setHeaderLabel('数据源')
    
            # 设置根结点
            root = QTreeWidgetItem(self)
            root.setText(0, '数据库')
            root.setIcon(0, QIcon('./images/database.png'))
            self.setColumnWidth(0, 100)
    
            self.child_DA = QTreeWidgetItem(root)
            self.child_DA.setText(0, 'DA表')
            self.child_DA.setIcon(0, QIcon('./images/folder.png'))
    
            self.child_TEST = QTreeWidgetItem(root)
            self.child_TEST.setText(0, '测试信息表')
            self.child_TEST.setIcon(0, QIcon('./images/folder.png'))
    
        def set_tree_children(self, da_table, test_table):
            for i in da_table:
                DA_table = QTreeWidgetItem(self.child_DA)
                DA_table.setText(0, str(i))
                DA_table.setIcon(0, QIcon('./images/table.png'))
    
            for i in test_table:
                table = QTreeWidgetItem(self.child_TEST)
                table.setText(0, str(i))
                table.setIcon(0, QIcon('./images/table.png'))
    
       
    
    
    
    class Data_Mainwindow(QMainWindow):
        def __init__(self):
            super().__init__()
            self.left_tree = BasicTreeWidget()
            self.table_view = BasicTableView()  ##后期进行改造
            self.sql_server = Database(server='192.168.64.105', user='sa', password='123456', database='OTPTrackDB')
            self.page = PageController(1)
            self.not_first = False  ##去除SkipController切换时的小bug
    
            self._init_ui()
    
        def set_menu(self):
            bar = self.menuBar()
    
            # Create Root Menus
            file = bar.addMenu('文件')
            edit = bar.addMenu('编辑')
    
            # file affairs
            save_action = QAction('保存', self)
            save_action.setShortcut('Ctrl+S')
            quit_action = QAction('&Quit', self)
            quit_action.setShortcut('Ctrl+Q')
    
            file.addAction(save_action)
            file.addAction(quit_action)
            quit_action.triggered.connect(self.quit_trigger)
    
    
            ###edit affairs
            find_action = QAction('查找...', self)
            find_action.setShortcut('Ctrl+F')
            edit.addAction(find_action)
            find_action.triggered.connect(self.find_module_info)
    
    
    
    
            settings_menu=edit.addMenu('settings')
            font_action=QAction('设置字体',self)
            font_color_action=QAction('设置字体颜色',self)
    
            settings_menu.addAction(font_action)
            settings_menu.addAction(font_color_action)
    
            font_action.triggered.connect(self.set_font)
            font_color_action.triggered.connect(self.set_font_color)
    
    
    
    
    
    
    
        def _init_ui(self):
            self.set_menu()
            ##新建一个widget，作为grid的容器，然后在里面放置Tree控件（后续这个widget又可以作为一个大包进行管理
            self.widget = QWidget()
            self.grid_layout = QGridLayout()
            self.widget.setLayout(self.grid_layout)
    
            self.left_tree.set_tree_children(*self.sql_server.get_all_tables())
            self.grid_layout.addWidget(self.left_tree, 0, 0)  # 向widget的网格中添加控件，而widget又添加到主界面中
    
    
            self.grid_layout.addWidget(self.table_view, 0, 1)
            self.setCentralWidget(self.widget)
    
            self.grid_layout.setSpacing(10)
            self.left_tree.setMaximumWidth(280)
    
            self.setWindowTitle("数据查询系统")
            self.setWindowIcon(QIcon('./little_pandas.ico'))
            self.resize(800, 600)
            self.show()
    
            ##分页事件的响应
            self.page.confirmSkip.clicked.connect(self.onSkipPage)
            self.page.prePage.clicked.connect(lambda: self.pre_next_page(-1))
            self.page.nextPage.clicked.connect(lambda: self.pre_next_page(1))
    
    
            ##树控件事件：右键弹框保存，打开
            self.left_tree.doubleClicked.connect(self.onTreedoubleClicked)
    
    
    
    
    
        def pre_next_page(self, offset):
    
            current_page = int(self.page.curPage.text())
            total_page = int(self.page.totalPage.text().split()[1])
            self.page.skipPage.setText('')
    
            skip_page = current_page + offset
            if skip_page < 1:
                return
            if skip_page > total_page:
                return
    
            self._search_table(self.current_table_name, skip_page)
            self.page.curPage.setText(str(skip_page))
    
        def onSkipPage(self):
            current_page = int(self.page.curPage.text())
            total_page = int(self.page.totalPage.text().split()[1])
            if '' == self.page.skipPage.text():
                skip_page = 0
            else:
                skip_page = int(self.page.skipPage.text())
                if skip_page < 0:
                    skip_page = 1
                    self.page.skipPage.setText(str(1))
    
            if skip_page > total_page:
                self.page.skipPage.setText(str(total_page))
                skip_page = total_page
    
            if current_page == skip_page:
                return
    
            if self.current_table_name:
                self._search_table(self.current_table_name, skip_page)
                self.page.curPage.setText(str(skip_page))
    
        def _search_table(self, table_name: str, skip_page=1):
            if 'tbl_' in table_name or 'DA_' in table_name:
                column_names, rows = self.sql_server.get_table_content(table_name, skip_page)
    
                is_trim = False
                if 'tbl_' in table_name:
                    is_trim = True
    
                    if self.not_first:
                        self.page.show()
    
                    self.grid_layout.addWidget(self.page, 1, 1)
                    page_number = self.sql_server.get_table_row_count(table_name)
                    self.not_first = True
    
                    if 0 == page_number:
                        page_number = page_number + 1
                    self.page_number = math.ceil(page_number / 200)
                    self.page.totalPage.setText('共 ' + str(self.page_number) + ' 页')
                    self.page.curPage.setText('1')
    
                    self.current_table_name = table_name
                else:
                    self.page.close()
                self.table_view.show_data(rows, column_names, is_trim)
    
        def onTreedoubleClicked(self, index):
            item = self.left_tree.currentItem()
            self.page.skipPage.setText('')
            self._search_table(item.text(0))
    
        def find_module_info(self):
            dialog = QDialog()
            button = QPushButton('确定', dialog)  # 此时的dialog相当于继承类中编写的self，在类中可默认不写
            button.clicked.connect(dialog.close)
    
            button.move(50, 50)
            dialog.setWindowTitle('查找')
            dialog.setWindowModality(Qt.ApplicationModal)
    
            dialog.exec_()
    
    
        def set_font(self):
            font,ok=QFontDialog.getFont()
            if ok:
                self.table_view.tableview.setFont(font)
    
        def set_font_color(self):
            color = QColorDialog.getColor()
            p = QPalette()
            p.setColor(QPalette.Text, color)
            self.table_view.tableview.setPalette(p)
    
    
    
    
    
    
        def quit_trigger(self):
            qApp.quit()
    
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        app.setWindowIcon(QIcon('./little_pandas.ico'))
        tree = Data_Mainwindow()
    
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
