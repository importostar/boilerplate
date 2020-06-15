---
title: accuradio_button
date: 2020-05-07
---
Example Python program accuradio_button.py

## Modules

* from splinter.browser import Browser
* import Tkinter
* import sys

## Classes

* class Radio():

## Methods

* def __init__(self):
* def goToChannel(self, channel=''):
* def playStop(self):
* def skipSong(self):
* def openMainWindow(self):
* def main(args):

## Code

Python tkinter example

    #!/usr/bin/python
    # -*- encoding: utf-8 -*-
    
    from splinter.browser import Browser
    import Tkinter
    import sys
    
    
    class Radio():
        def __init__(self):
            self.b = Browser('chrome')
            self.play_stop_button = None
            self.skip_button = None
    
        def goToChannel(self, channel=''):
            if channel:
                self.b.visit('http://www.accuradio.com/#!/search/{0}/'.format(channel))
                self.b.find_by_name(channel).first.click()
            else:
                self.b.visit('http://www.accuradio.com/')
    
        def playStop(self):
            if not self.play_stop_button:
                if self.b.is_element_present_by_id('pause_button'):
                    self.play_stop_button = self.b.find_by_id('pause_button')
                    self.play_stop_button.first.click()
            else:
                self.play_stop_button.first.click()
    
        def skipSong(self):
            if not self.skip_button:
                if self.b.is_element_present_by_id('skip_button'):
                    self.skip_button = self.b.find_by_id('skip_button')
                    self.skip_button.first.click()
            else:
                self.skip_button.first.click()
    
        def openMainWindow(self):
            self.root = Tkinter.Tk()
            self.root.call('wm', 'attributes', '.', '-topmost', '1')
            self.root.title('Accuradio')
            self.root.geometry('80x50')
            self.play_stop_button = Tkinter.Button(master=self.root, text='Play/Stop', command=self.playStop).pack()
            self.skip_button = Tkinter.Button(master=self.root, text='Skip', command=self.skipSong).pack()
            self.root.mainloop()
    
    def main(args):
        radio = Radio()
        if len(args) == 1:
            radio.goToChannel(channel=args[0])
        else:
            radio.goToChannel()
        radio.openMainWindow()
    
    
    if __name__ == '__main__':
        main(sys.argv[1:])
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
