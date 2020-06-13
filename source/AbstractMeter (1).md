---
title: AbstractMeter (1)
date: 2020-05-07
---
Example Python program AbstractMeter (1).py

## Modules

* from BackgroundWidget import BackgroundWidget

## Classes

* class AbstractMeter(BackgroundWidget):

## Methods

* def __init__(self, parent=None):
* def critical(self):
* def setCritical(self, val):
* def nominal(self):
* def setNominal(self, val):
* def minimal(self):
* def setMinimal(self, val):
* def maximal(self):
* def setMaximal(self, val):
* def value(self):
* def setValue(self, val):

## Code

Python example

    # -*- coding: utf-8 -*-
    
    from BackgroundWidget import BackgroundWidget
    
    
    class AbstractMeter(BackgroundWidget):
        def __init__(self, parent=None):
            BackgroundWidget.__init__(self, parent=parent)
    
            self.mValue = 0.0
            self.mMinimal = 0.0
            self.mNominal = 25
            self.mCritical = 75
            self.mMaximal = 100
    
        def critical(self):
            return self.mCritical
    
        def setCritical(self, val):
            if self.mCritical != val:
                self.mCritical = val
                self.mModified = True
                self.update()
    
        def nominal(self):
            return self.mNominal
    
        def setNominal(self, val):
            if self.mNominal != val:
                self.mNominal = val
                self.mModified = True
                self.update()
    
        def minimal(self):
            return self.mMinimal
    
        def setMinimal(self, val):
            if self.mMinimal != val:
                self.mMinimal = val
                self.mModified = True
                self.update()
    
        def maximal(self):
            return self.mMaximal
    
        def setMaximal(self, val):
            if self.mMaximal != val:
                self.mMaximal = val
                self.mModified = True
                self.update()
    
        def value(self):
            return self.mValue
    
        def setValue(self, val):
            if self.mValue != val:
                self.mValue = val
                self.update()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
