---
title: texture_id_leak (1)
date: 2020-05-07
---
Example Python program texture_id_leak (1).py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* from kivy.app import App
* from kivy.uix.floatlayout import FloatLayout
* from kivy.uix.label import Label
* from kivy.clock import Clock
* from kivy.uix.button import Button

## Classes

* class TestApp(App):

## Methods

* def redraw(self, dt = None):
* def build(self):

## Code

Python example

    from kivy.app import App
    from kivy.uix.floatlayout import FloatLayout
    from kivy.uix.label import Label
    from kivy.clock import Clock
    from kivy.uix.button import Button
    
    class TestApp(App):
        def redraw(self, dt = None):
            self.lbl.text = "hello %d"%self.count
            self.lbl.texture_update()
            print "texture id:", self.lbl.texture.id
            self.count += 1
            Clock.schedule_once(self.redraw)
    
        def build(self):
            self.count = 0
            self.layout = FloatLayout()
            
            lbl = Label(size=(100,100), size_hint=(None,None), markup = True, halign = "center")
            lbl.text = "starting..."
            lbl.color = (1,0,0,1)
            lbl.pos = (20, 20)
            #lbl.text_size = (120, 60) #Work around for very elusive texture id kivy bug
            lbl.texture_update()
            self.lbl = lbl
            self.layout.add_widget(Button(text='Hello World'))
            self.layout.add_widget(self.lbl)
            
            self.redraw()
            return self.layout
    
    TestApp().run()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
