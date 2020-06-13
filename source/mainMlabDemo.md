---
title: mainMlabDemo
date: 2020-05-07
---
Example Python program mainMlabDemo.py
This program creates a PyQt GUI

## Modules

* import sys 
* from PyQt5.QtWidgets import *
* from PyQt5.QtGui import QIcon # import function cho phép tải icon cho giao diện 
* from MlabDemo import MlabDemo # import đối tượng MlabDemo đã tạo ra trong module MlabDemo 

## Classes

* class MainScreen(QWidget):

## Methods

* 	def __init__(self):
* 	def center(self):	# định nghĩa hàm center() 

## Code

Example Python PyQt program :

    import sys 
    from PyQt5.QtWidgets import *
    from PyQt5.QtGui import QIcon # import function cho phép tải icon cho giao diện 
    from MlabDemo import MlabDemo # import đối tượng MlabDemo đã tạo ra trong module MlabDemo 
    
    class MainScreen(QWidget):
    	def __init__(self):
    		super(MainScreen, self).__init__()
    		self.ui = MlabDemo() 				   # tạo một GUI với đối tượng là giao diện MlabDemo đã thiết kế
    		self.ui.setupUi(self)
    		self.setWindowTitle('Mlab GUI Demo')   # đặt tiêu đề cho giao diện 
    		self.setWindowIcon(QIcon("mlab2.ico")) # tải icon cho giao diện 
    		self.center()						   # hàm center() giúp đưa giao diện vào giữa màn hình 
    
    	def center(self):	# định nghĩa hàm center() 
    		qr = self.frameGeometry()  # nhận một cửa sổ hình chữ nhật mô tả màn hình chính của giao diện
    		cp = QDesktopWidget().availableGeometry().center() # tính toán độ phân giải và tìm ra điểm giữa của màn hình
    		qr.moveCenter(cp) # di chuyển điểm giữa của hình chữ nhật tới trùng với điểm giữa của màn hình, 
    						  # giữ cho kích thước hình chữ nhật không đổi
    		self.move(qr.topLeft()) # di chuyển màn hình chính của giao diện tới vị trí cửa sổ hình chữ nhật (ở giữa màn hình)
    		
    # chương trình chính 	
    app = QApplication(sys.argv) # tạo một đối tượng ứng dụng 
    myapp = MainScreen() 		 # gọi cửa sổ chứa giao diện chính 
    myapp.show()				 # hiển thị giao diện lên màn hình 
    sys.exit(app.exec_())		 # thực hiện vòng lặp chính của chương trình 

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
