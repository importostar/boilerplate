---
title: pyqt5_network_info
date: 2020-05-07
---
Example Python program pyqt5_network_info.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtWidgets import QDialog, QGridLayout, QLabel, QPushButton
* from PyQt5.QtNetwork import QNetworkInterface, QAbstractSocket
* from PyQt5.QtWidgets import QApplication

## Classes

* class NetworkInfoDialog(QDialog):

## Methods

* def __init__(self, parent=None):
* def get_interfaces(self):

## Code

Example Python PyQt program :

    from PyQt5.QtWidgets import QDialog, QGridLayout, QLabel, QPushButton
    from PyQt5.QtNetwork import QNetworkInterface, QAbstractSocket
    
    
    class NetworkInfoDialog(QDialog):
        def __init__(self, parent=None):
            super().__init__(parent)
            self.setWindowTitle('Network Interface Info')
            layout = QGridLayout(self)
            for i, interface in enumerate(self.get_interfaces()):
                if 'ipv4' in interface or 'ipv6' in interface:
                    layout.addWidget(QLabel(interface['name']), i, 0)
                    layout.addWidget(QLabel(interface.get('ipv4', '')), i, 1)
                    layout.addWidget(QLabel(interface.get('ipv6', '')), i, 2)
    
            ok_button = QPushButton('OK')
            ok_button.clicked.connect(self.accept)
            layout.addWidget(ok_button, i + 1, 0, -1, -1)
    
        def get_interfaces(self):
            """Return IPv4 and IPv6 addresses for all network interfaces."""
            for interface in QNetworkInterface.allInterfaces():
                connection = {'name': interface.humanReadableName()}
                for address in interface.addressEntries():
                    ip = address.ip()
                    if ip.protocol() == QAbstractSocket.IPv4Protocol:
                        connection['ipv4'] = ip.toString()
                    elif ip.protocol() == QAbstractSocket.IPv6Protocol:
                        connection['ipv6'] = ip.toString()
                yield connection
    
    
    if __name__ == '__main__':
        from PyQt5.QtWidgets import QApplication
    
        app = QApplication([])
        widget = NetworkInfoDialog()
        widget.show()
        app.exec_()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
