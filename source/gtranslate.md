---
title: gtranslate
date: 2020-05-07
---
Example Python program gtranslate.py

## Modules

* import Tkinter as tkinter
* import urllib2, urllib
* import json

## Classes

* class TranlateFrame(tkinter.Frame, object):

## Methods

* def translate(lang_pair, word):
* def __init__(self, parent):
* def translate(self, lang_pair):
* def trans(*args):

## Code

Python tkinter example

    # -*- coding: iso-8859-15 -*-
    
    import Tkinter as tkinter
    import urllib2, urllib
    import json
    
    TRANSLATE_URL = 'http://ajax.googleapis.com/ajax/services/language/translate'
    
    TO_ENGLISH = 'fr|en'
    TO_FRENCH = 'en|fr'
    
    
    def translate(lang_pair, word):
        params = { 'v': '1.0',
                 'langpair': lang_pair,
                 'q': word }  
        
        url = TRANSLATE_URL + '?' + urllib.urlencode(params)
        response = json.loads(urllib2.urlopen(url).read())
        return response['responseData']['translatedText']
        
        
    class TranlateFrame(tkinter.Frame, object):
        
        def __init__(self, parent):
            super(TranlateFrame, self).__init__(parent)
    
            tkinter.Label(self, text='Enter text').grid(row=0, column=0)
            
            self.word_to_translate = tkinter.StringVar()
            self.entry = tkinter.Entry(self, textvariable=self.word_to_translate)
            self.entry.grid(row=0, column=1, columnspan=2)
            
            tkinter.Button(self, text='In english', 
                            command=self.translate(TO_ENGLISH), 
                            underline=3).grid(row=1, column=1)
                
            tkinter.Button(self, text='En français', 
                            command=self.translate(TO_FRENCH), 
                            underline=3).grid(row=1, column=2)
            
            parent.bind('<Alt_L> <e>', self.translate(TO_ENGLISH))
            parent.bind('<Alt_L> <f>', self.translate(TO_FRENCH))
    
            self.entry.focus()
    
    
        def translate(self, lang_pair):
            def trans(*args):
                translated = translate(lang_pair, self.word_to_translate.get().strip())
                self.word_to_translate.set(translated)
            return trans
    
        
    if __name__ == '__main__':
        root = tkinter.Tk()
        root.title('Google translate')
        
        f = TranlateFrame(root)
        f.pack()
        
        root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
