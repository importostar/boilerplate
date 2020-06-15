---
title: osc
date: 2020-05-07
---
Example Python program osc.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from PyQt5.QtCore import (
* from PyQt5.QtWidgets import (
* from pythonosc import (
* import threading

## Classes

* class MainWindow(QMainWindow):
* class SendWidget(QWidget):
* class ReceiveWidget(QWidget):
* 		class Communicate(QObject):

## Methods

* 	def __init__(self):
* 	def initUI(self):
* 	def closeEvent(self, event):
* 	def __init__(self):
* 	def initUI(self):
* 	def send(self):
* 	def __init__(self):
* 	def initUI(self):
* 	def receive(self):
* 		def handleReceivedMessage(addr, data):

## Code

Example Python PyQt program :

    import sys
    
    from PyQt5.QtCore import (
    	pyqtSignal,
    	QObject
    )
    
    from PyQt5.QtWidgets import (
    	QMainWindow,
    	QWidget,
    	QPushButton,
    	QLabel,
    	QLineEdit,
    	QTextEdit,
    	QVBoxLayout,
    	QHBoxLayout,
    	QGridLayout,
    	QApplication
    )
    
    from pythonosc import (
    	osc_message_builder,
    	udp_client,
    	dispatcher,
    	osc_server
    )
    
    import threading
    
    class MainWindow(QMainWindow):
    
    	def __init__(self):
    		super().__init__()
    		self.initUI()
    
    	def initUI(self):
    		self.sendWidget = SendWidget()
    		self.receiveWidget = ReceiveWidget()
    
    		layout = QVBoxLayout()
    		layout.setSpacing(20)
    		layout.addWidget(self.sendWidget)
    		layout.addWidget(self.receiveWidget)
    
    		centralWidget = QWidget()
    		centralWidget.setLayout(layout)
    		self.setCentralWidget(centralWidget)
    
    		self.setGeometry(100, 100, 250, 300)
    		self.setWindowTitle("OSC: SEND / RECEIVE")
    		self.show()
    
    	def closeEvent(self, event):
    		print("closing")
    		if self.receiveWidget.serverRunning:
    			print("ReceiveWidget, deleting thread")
    			self.receiveWidget.server.shutdown()
    			self.receiveWidget.server.server_close()
    			self.receiveWidget.serverRunning = False
    
    
    class SendWidget(QWidget):
    
    	def __init__(self):
    		super().__init__()
    		self.initUI()
    
    	def initUI(self):
    		labelIP = QLabel("SEND IP", self)
    		self.IPEdit = QLineEdit()
    		self.IPEdit.setText("127.0.0.1")
    		labelPort = QLabel("SEND PORT", self)
    		self.portEdit = QLineEdit()
    		self.portEdit.setText("8000")
    		labelAddress = QLabel("SEND ADDRESS", self)
    		self.addressEdit = QLineEdit()
    		self.addressEdit.setText("debug")
    		labelData = QLabel("SEND DATA")
    		self.dataEdit = QLineEdit()
    		self.dataEdit.setText("1")
    		button = QPushButton("SEND", self)
    
    		button.clicked.connect(self.send)
    		
    		grid = QGridLayout();
    		grid.setColumnMinimumWidth(0, 100)
    
    		grid.addWidget(labelIP, 1, 0)
    		grid.addWidget(self.IPEdit, 1, 1)
    
    		grid.addWidget(labelPort, 2, 0)
    		grid.addWidget(self.portEdit, 2, 1)
    
    		grid.addWidget(labelAddress, 3, 0)
    		grid.addWidget(self.addressEdit, 3, 1)
    
    		grid.addWidget(labelData, 4, 0)
    		grid.addWidget(self.dataEdit, 4, 1)
    
    		grid.addWidget(button, 5, 1)
    
    		self.setLayout(grid)
    		self.show()
    
    	def send(self):
    		if self.IPEdit.text() == "" or self.portEdit.text() == "" or self.addressEdit.text() == "":
    			print("ip, port or address empty")
    			return
    
    		client = udp_client.UDPClient(self.IPEdit.text(), int(self.portEdit.text()))
    		msg = osc_message_builder.OscMessageBuilder(address = "/" + self.addressEdit.text())
    		msg.add_arg(self.dataEdit.text())
    		msg = msg.build()
    		client.send(msg)
    
    
    class ReceiveWidget(QWidget):
    
    	serverRunning = False
    	runningIP = ""
    	runningPort = 0
    
    	def __init__(self):
    		super().__init__()
    		self.initUI()
    
    	def initUI(self):
    		labelIP = QLabel("RECEIVE IP", self)
    		self.IPEdit = QLineEdit()
    		self.IPEdit.setText("127.0.0.1")
    		labelPort = QLabel("RECEIVE PORT", self)
    		self.portEdit = QLineEdit()
    		self.portEdit.setText("8000")
    		button = QPushButton("RECEIVE", self)
    
    		grid = QGridLayout()
    		grid.setColumnMinimumWidth(0, 100)
    		grid.addWidget(labelIP, 0, 0)
    		grid.addWidget(self.IPEdit, 0, 1)
    		grid.addWidget(labelPort, 1, 0)
    		grid.addWidget(self.portEdit, 1, 1)
    		grid.addWidget(button, 2, 1)
    		
    		labelAddress = QLabel("ADDRESS", self)
    		self.receivedAddress = QTextEdit()
    		addressBox = QVBoxLayout()
    		addressBox.addWidget(labelAddress)
    		addressBox.addWidget(self.receivedAddress)
    
    		labelData = QLabel("DATA")
    		self.receivedData = QTextEdit()
    		dataBox = QVBoxLayout()
    		dataBox.addWidget(labelData)
    		dataBox.addWidget(self.receivedData)
    
    		receiveBox = QHBoxLayout()
    		receiveBox.addLayout(addressBox)
    		receiveBox.addLayout(dataBox)
    
    		box = QVBoxLayout()
    		box.addLayout(grid)
    		box.addLayout(receiveBox)
    		self.setLayout(box)
    
    		button.clicked.connect(self.receive)
    		self.show()
    
    	def receive(self):
    		if self.serverRunning:
    			print("server already running")
    			self.server.shutdown()
    			self.server.server_close()
    
    		ip = self.IPEdit.text()
    		port = int(self.portEdit.text())
    
    		class Communicate(QObject):
    			receive = pyqtSignal(object, object)
    
    		def handleReceivedMessage(addr, data):
    			print(addr, ":", data)
    			self.receivedAddress.append(addr)
    			self.receivedData.append(data)
    
    		self.c = Communicate()
    		self.c.receive.connect(handleReceivedMessage)
    
    		myDispatcher = dispatcher.Dispatcher()
    		# myDispatcher.set_default_handler(handleReceivedMessage)
    		myDispatcher.set_default_handler(self.c.receive.emit)
    
    		self.server = osc_server.ThreadingOSCUDPServer((ip, port), myDispatcher)
    		server_thread = threading.Thread(target=self.server.serve_forever)
    		server_thread.start()
    		print("thread start")
    
    		self.serverRunning = True
    		self.runningIP = ip
    		self.runningPort = port
    
    
    if __name__ == "__main__":
    	app = QApplication(sys.argv)
    	win = MainWindow()
    	sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
