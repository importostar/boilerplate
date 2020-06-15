---
title: KPDR900_serial
date: 2020-05-07
---
Example Python program KPDR900_serial.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import serial
* import logging

## Classes

* class KPDR900:

## Methods

* def __init__(self,ser,addr = 1,logfile="KPDR900_default.log"):
* def read(self):
* def write(self,msg):

## Code

Python example

    import serial
    import logging
    
    port = "COM1"
    baudrate = 19200
    timeout = 5
    
    class KPDR900:
        term = b";FF"
        def __init__(self,ser,addr = 1,logfile="KPDR900_default.log"):
           logging.basicConfig(format='%(asctime)s %(levelname)s:%(message)s', 
                               filename=logfile, level = logging.DEBUG)
           self.addr = addr
           self.ser = ser
           self.prefix = b"@%03d" % self.addr
           logging.info("KPDR900 Initialized with serial "+str(self.ser)+" and address "+str(self.addr))
    
        def read(self):
            msg = b''
            while not msg.endswith(KPDR900.term):
                r = self.ser.read()
                if len(r) == 0:
                    break
                msg += r
            logging.info("Read: "+str(msg))
            if b'ACK' not in msg:
                logging.warning("Response did not include ACK!")
            return msg
    
        def write(self,msg):
            if not msg.startswith(self.prefix):
                msg = self.prefix + msg
            if not msg.endswith(KPDR900.term):
                msg += KPDR900.term
            self.ser.write(msg)
            logging.info("Write: "+str(msg))
    
    if __name__ == "__main__":
        ser = serial.Serial(port=port,baudrate=baudrate,timeout=timeout)
        pdr = KPDR900(ser)
        pdr.write(b'SNC?') # Ask for serial number
        print(pdr.read())
        
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
