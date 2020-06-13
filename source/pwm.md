---
title: pwm
date: 2020-05-07
---
Example Python program pwm.py

## Modules

* import sys
* import tkinter
* import wiringpi

## Classes

* class Led:
* class App:

## Methods

* def __init__(self):
* def initialize(self):
* def startPwm(self):
* def flushPwm(self):
* def stopPwm(self):
* def setEnabled(self, isEnabled):
* def setBrightness(self, brightness):
* def __init__(self):
* def onRadioVarChanged(self):
* def onScaleVarChanged(self, value):
* def initializeLabel(self):
* def initializeRadiobutton(self, text, value):
* def initializeRadiobuttons(self):
* def initializeScale(self):
* def initializeButton(self):
* def initialize(self):
* def show(self):
* def main(self):

## Code

Python tkinter example

    import sys
    import tkinter
    import wiringpi
    
    LED_GPIO = 26
    PWM_MAX = 100
    
    class Led:
        def __init__(self):
            self.isEnabled = False
            self.brightness = 0
        
        def initialize(self):
            wiringpi.wiringPiSetupGpio()
            wiringpi.pinMode(LED_GPIO, 1)
        
        def startPwm(self):
            wiringpi.softPwmCreate(LED_GPIO, self.brightness, PWM_MAX)
        
        def flushPwm(self):
            wiringpi.softPwmWrite(LED_GPIO, self.brightness)
        
        def stopPwm(self):
            wiringpi.softPwmStop(LED_GPIO)
            
        def setEnabled(self, isEnabled):
            if self.isEnabled == False and isEnabled == True:
                self.startPwm()
            elif self.isEnabled == True and isEnabled == False:
                self.stopPwm()
            self.isEnabled = isEnabled
        
        def setBrightness(self, brightness):
            self.brightness = brightness
            if self.isEnabled == True:
                self.flushPwm()
            
    class App:
        def __init__(self):
            self.led = Led()
            self.led.initialize()
            self.window = tkinter.Tk()
            
        def onRadioVarChanged(self):
            self.led.setEnabled(self.radioVar.get())
        
        def onScaleVarChanged(self, value):
            self.led.setBrightness(self.scaleVar.get())
    
        def initializeLabel(self):
            label = tkinter.Label(self.window, text = "LEDスイッチ")
            label.grid(row = 0, columnspan = 2)
        
        def initializeRadiobutton(self, text, value):
            return tkinter.Radiobutton(
                self.window,
                text = text,
                variable = self.radioVar,
                value = value,
                command = self.onRadioVarChanged
            )
        
        def initializeRadiobuttons(self):
            self.radioVar = tkinter.BooleanVar()
            self.initializeRadiobutton("OFF", False).grid(row = 1, column = 0)
            self.initializeRadiobutton("ON", True).grid(row = 1, column = 1)
            
        def initializeScale(self):
            self.scaleVar = tkinter.IntVar()
            tkinter.Scale(
                self.window,
                label = "明るさ",
                orient = "h",
                from_ = 0,
                to = 100,
                variable = self.scaleVar,
                command = self.onScaleVarChanged
            ).grid(row = 2, columnspan = 2)
        
        def initializeButton(self):
            tkinter.Button(
                self.window,
                text = "終了",
                command = sys.exit
            ).grid(row = 3, columnspan = 2)
        
        def initialize(self):
            self.initializeLabel()
            self.initializeRadiobuttons()
            self.initializeScale()
            self.initializeButton()
        
        def show(self):
            self.window.mainloop()
        
        def main(self):
            self.initialize()
            self.show()
    
    if __name__ == "__main__":
        App().main()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
