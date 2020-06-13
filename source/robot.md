---
title: robot
date: 2020-05-07
---
Example Python program robot.py

## Modules

* import RPi.GPIO as gpio
* import time

## Methods

* def init():
* def fw(tf):
* def rv(tf):
* def pvr(tf):
* def pvl(tf):
* def sensordist():  
* def servoinit():
* def servomid():
* def servofullright():
* def servofullleft():

## Code

Python example

    import RPi.GPIO as gpio
    import time
    
    #sensor pins
    trig_pin=12
    echo_pin=16
    
    # servo pin
    servo_pin=18
    
    
    # motor control
    
    def init():
        gpio.setmode(gpio.BOARD)
        gpio.setup(7, gpio.OUT)
        gpio.setup(11, gpio.OUT)
        gpio.setup(13, gpio.OUT)
        gpio.setup(15, gpio.OUT)
    
    def fw(tf):
        init()
        gpio.output(7,  True)    # motor 1 (left)
        gpio.output(11, False)
        gpio.output(13, True)    # motor 2 (right) 
        gpio.output(15, False)
        time.sleep(tf)
        gpio.cleanup()
    
    
    def rv(tf):
        init()
        gpio.output(7, False)    # motor 1 (left)
        gpio.output(11, True)
        gpio.output(13, False)    # motor 2 (right) 
        gpio.output(15, True)
        time.sleep(tf)
        gpio.cleanup()
    
    
    #pivot right
    def pvr(tf):
        init()
        gpio.output(7,  True)     # motor 1 (left) fw
        gpio.output(11, False)
        gpio.output(13, False)    # motor 2 (right) rv 
        gpio.output(15, True)
        time.sleep(tf)
        gpio.cleanup()
    
    
    # pivot left    
    def pvl(tf):
        init()
        gpio.output(7,  False)    # motor 1 (left) rv
        gpio.output(11, True)
        gpio.output(13, True)     # motor 2 (right) fw 
        gpio.output(15, False)
        time.sleep(tf)
        gpio.cleanup()
    
    ############################################################
    
    # sensor functions
    
    def sensordist():  
        gpio.setmode(gpio.BOARD)
        gpio.setup(trig_pin, gpio.OUT)
        gpio.sdtup(echo_pin, gpio.IN)
        
        gpio.output(trig_pin, False)
        time.sleep(0.2)
        gpio.output(trig_pin, True)
        
        while gpio.input(echo_pin)==False:
            starttm=time.time()
        
        while gpio.input(echo_pin)==True:
            endtm=time.time()
    
        elaptm=endtm-starttm
    
        distance=elaptm * 17000  # distance in cm
    
        gpio.cleanup()
        return distance
    
    #########################################################
    
    # servo functions
    def servoinit():
        gpio.setmode(gpio.BOARD)
        gpio.setup(servo_pin, gpio.OUT)
        sp=gpio.PWM(servo_pin, 50)
    
        
    def servomid():
        servoinit()
        sp.ChangeDutyCycle(7.5)
        time.sleep(.1)
        sp.stop()
        gpio.cleanup()
    
    def servofullright():
        servoinit()
        sp.ChangeDutyCycle(12.5)
        time.sleep(.1)
        sp.stop()
        gpio.cleanup()
    
    def servofullleft():
        servoinit()
        sp.ChangeDutyCycle(2.5)
        time.sleep(.1)
        sp.stop()
        gpio.cleanup()
    
    
    # main Block of Code
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
