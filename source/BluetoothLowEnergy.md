---
title: BluetoothLowEnergy
date: 2020-05-07
---
Example Python program BluetoothLowEnergy.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import PyQt5
* from PyQt5 import QtCore
* from PyQt5 import QtBluetooth
* import sys

## Classes

* class DeviceFinder(QtCore.QObject):

## Methods

* def __init__(self):
* def add_device(self, device):
* def scan_finished(self):
* def scan_error(self):
* def quit(self):

## Code

Example Python PyQt program :

    import PyQt5
    from PyQt5 import QtCore
    from PyQt5 import QtBluetooth
    
    
    class DeviceFinder(QtCore.QObject):
        def __init__(self):
            super().__init__()
            self.m_devices = []
    
            self.deviceDiscoveryAgent = QtBluetooth.QBluetoothDeviceDiscoveryAgent(self)
            self.deviceDiscoveryAgent.setLowEnergyDiscoveryTimeout(500)
            self.deviceDiscoveryAgent.deviceDiscovered.connect(self.add_device)
            self.deviceDiscoveryAgent.error.connect(self.scan_error)
            self.deviceDiscoveryAgent.finished.connect(self.scan_finished)
            self.deviceDiscoveryAgent.canceled.connect(self.scan_finished)
    
            self.deviceDiscoveryAgent.start(QtBluetooth.QBluetoothDeviceDiscoveryAgent.DiscoveryMethod(2))
    
        def add_device(self, device):
            # If device is LowEnergy-device, add it to the list
            if device.coreConfigurations() and QtBluetooth.QBluetoothDeviceInfo.LowEnergyCoreConfiguration:
                self.m_devices.append( QtBluetooth.QBluetoothDeviceInfo(device) )
                print("Low Energy device found. Scanning more...")
    
        def scan_finished(self):
            print("scan finished")
            for i in self.m_devices:
                #QtBluetooth.QBluetoothDeviceInfo.
                print('UUID: {UUID}, Name: {name}, rssi: {rssi}'.format(UUID=i.deviceUuid().toString(),
                                                                        name=i.name(),
                                                                        rssi=i.rssi()))
            self.quit()
    
        def scan_error(self):
            print("scan error")
    
        def quit(self):
            print("Bye!")
            QtCore.QCoreApplication.instance().quit()
    
    
    if __name__ == "__main__":
        import sys
        app = QtCore.QCoreApplication(sys.argv)
        hello = DeviceFinder()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
