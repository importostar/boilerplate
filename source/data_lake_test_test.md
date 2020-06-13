---
title: data_lake_test_test
date: 2020-05-07
---
Example Python program data_lake_test_test.py
This program creates a PyQt GUI

## Modules

* import sys
* from data_lake.gui.resource.home import Ui_MainWindow
* from data_lake.gui.panels import *
* from PyQt5.QtWidgets import QApplication,QMainWindow,QStackedLayout

## Classes

* class MyMainWindow(QMainWindow,Ui_MainWindow):

## Methods

* def __init__(self):
* def show_panel(self):

## Code

Example Python PyQt program :

    import sys
    from data_lake.gui.resource.home import Ui_MainWindow
    from data_lake.gui.panels import *
    from PyQt5.QtWidgets import QApplication,QMainWindow,QStackedLayout
    
    
    class MyMainWindow(QMainWindow,Ui_MainWindow):
        def __init__(self):
            super(MyMainWindow,self).__init__()
            self.setupUi(self)
    
            self.qsl = QStackedLayout(self.frame_2)
            dashboard_panel  = DashboardPanel()
            data_source_panel = DataSourcePanel()
            schema_discovery_panel = SchemaDiscoveryPanel()
            schema_matching_panel = SchemaMatchingPanel()
            schema_summary_panel = SchemaSummaryPanel()
            queries_panel = QueriesPanel()
            data_quality_panel = DashboardPanel()
            about_panel = AboutPanel()
    
            self.qsl.addWidget (dashboard_panel)
            self.qsl.addWidget(data_source_panel)
            self.qsl.addWidget(schema_discovery_panel)
            self.qsl.addWidget (schema_matching_panel)
            self.qsl.addWidget (schema_summary_panel)
            self.qsl.addWidget (queries_panel)
            self.qsl.addWidget (data_quality_panel)
            self.qsl.addWidget (about_panel)
    
        def show_panel(self):
            dic = {'dashboard':0,
                   'data_source':1,
                   'schema_discovery': 2,
                   'schema_matching': 3,
                   'schema_summary': 4,
                   'queries': 5,
                   'data_quality': 6,
                   'about': 7}
            index = dic[self.sender().objectName()]
            self.qsl.setCurrentIndex(index)
    
    
    
    
    if __name__ == '__main__':
        app = QApplication([])
        main_window = MyMainWindow()
        main_window.show()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
