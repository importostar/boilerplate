---
title: Russian_Trainer (1)
date: 2020-05-07
---
Example Python program Russian_Trainer (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os
* import datetime
* import itertools
* from tkinter import *
* from tkinter import _tkinter  # for errors
* from tkinter.ttk import *
* from tkinter.messagebox import *
* from tkinter.scrolledtext import ScrolledText
* import requests
* from bs4 import BeautifulSoup
* import sys

## Classes

* class PronunciationGuide(ScrolledText):
* class Flashcard(Label): 
* class WotdGui(Frame):

## Methods

* def __init__(self, *args, **kwargs):
* def __init__(self, *args, **kwargs):
* def toggle_text(self, event=None):
* def __init__(self, *args, **kwargs):
* def show_guide(self, event=None):
* def render_wotd(self):
* def save_timestamp(t):
* def load_timestamp():
* def next_timestamp(current_date=None):
* def check_timestamp():
* def show_error(msg):
* def init_tk():
* def get_wotd():
* def wotd_cli(wotd):
* def wotd_gui(wotd):
* def main():

## Code

Python tkinter example

    #!python3
    # coding: utf-8
    
    import os
    import datetime
    import itertools
    
    from tkinter import *
    from tkinter import _tkinter  # for errors
    from tkinter.ttk import *
    from tkinter.messagebox import *
    from tkinter.scrolledtext import ScrolledText
    
    import requests
    from bs4 import BeautifulSoup
    
    
    __all__ = ['wotd_cli', 'wotd_gui', 'get_wotd']
    
    
    TIMESTAMP_FILE_NAME = 'wotd-timestamp'
    
    __TEST_WOTD = {
        'word': 'стильный', 
        'meaning': 'stylish, classy, trendy', 
        'phonetic': "[STEEL'-niy]", 
        'examples': [
            (
                'Жа́нна лю́бит сти́льную оде́жду.', 
                'Zhanna loves stylish clothes.'
            ), 
            (
                'Андре́й купи́л сти́льные чёрные очки́.', 
                'Andrey bought stylish black glasses.'
            ), 
            (
                'У Ната́ши сти́льная су́мка.', 
                'Natasha has a stylish handbag.'
            ), 
            (
                'Он был о́чень сти́льным челове́ком.', 
                'He was a very stylish person.'
            ),
        ]
    }
    
    PRONUNCIATION_GUIDE = '''
    A A - "A"
    K k - "K" 
    M m - "M"
    O o - "O"
    T t - "T"
    В в - "V"
    Е е - "yë"
    Н н - "N"
    Р р - "R"
    С с - "S"
    У у - "oo" (as in "spoon")
    Х х - "gutteral H as in 'Bach' or 'Loch'"
    Б б - "B"
    Г г - "G"
    Д д - "D"
    З з - "Z"
    И и - "Ē" "ee"
    Л л - "L"
    П п - "P"
    Ф ф - "F"
    Э э - "Ë"
    Ю ю - "you"
    Я я - "yä"
    Ё ё - "yo"
    Ж ж - "zh"
    Ц ц - "ts"
    Ч ч - "ch"
    Ш ш - "sh"
    
    Щ щ - Pronounced like "sh" but with your tongue on the roof of your mouth. Try putting your tongue in the same position as you would to say "ch" but say "sh" instead. English speakers may find it hard to define the difference between "ш" and "щ".
    
    Ы ы - Pronounced like the "i" in "bit" or "ill". (Said with your tongue slightly back in your mouth.)
    
    Й й - This letter is used to form diphthongs. So "oй" is like the "oy" sound in "boy" or "aй" is like the "igh" in "sigh".
    
    
    Ъ ъ - The 'Hard Sign' is rarely used. It indicates a slight pause between sylables.
    
    Ь ь - The 'Soft Sign' makes the previous letter 'soft'. Think of the "p" sound in the word "pew". (Try inflecting a very slight "y" sound onto letter before it.) 
    '''
    
    
    class PronunciationGuide(ScrolledText):
        def __init__(self, *args, **kwargs):
            super().__init__(*args, **kwargs)
            self.insert(1.0, PRONUNCIATION_GUIDE)
            self.configure(state=DISABLED)
            
        
        
    
    
    class Flashcard(Label): 
        def __init__(self, *args, **kwargs):
            self._text = kwargs.pop('text', '')
            self._answer = kwargs.pop('answer', '')
            
            super().__init__(*args, **kwargs)
            
            self._textvar = StringVar()
            self.configure(textvar=self._textvar)
            self._textvar.set(self._text)
            
            self._text_values = itertools.cycle([self._answer, self._text])
            self.bind('<Button-1>', self.toggle_text)
            
        def toggle_text(self, event=None):
            self._textvar.set(next(self._text_values))
            
        
    
    class WotdGui(Frame):
        def __init__(self, *args, **kwargs):
            self.wotd = kwargs.pop('wotd')
            super().__init__(*args, **kwargs)
            self.render_wotd()
            
            Frame(self).pack(expand=True, fill=Y)  # spacer for guide placement
            
            self.guide = Label(self, text='cyrillic guide')
            self.guide.bind('<Button-1>', self.show_guide)
            self.guide.pack(anchor='e')
            
            self._root().geometry('700x500')
        
        def show_guide(self, event=None):
            top = Toplevel(self._root())
            PronunciationGuide(top).pack(expand=True, fill=BOTH)
        
        def render_wotd(self):
            Label(
                self, 
                text=self.wotd['word'].title(), 
                style='Big.TLabel',
            ).pack()
            
            Label(
                self, 
                text=self.wotd['meaning'], 
                style='G.TLabel',
            ).pack()
            
            Flashcard(
                self, 
                text='<pronunciation>', 
                answer=self.wotd['phonetic'],
                style='G.TLabel',
            ).pack()
            
            for sentence in self.wotd['examples']:
                Flashcard(
                    self, 
                    text=sentence[0], 
                    answer=sentence[1],
                    style='Med.TLabel',
                ).pack()
            
            
    def save_timestamp(t):
        '''
        time stamp saved in ISO format as a string
        '''
        with open(TIMESTAMP_FILE_NAME, 'w') as f:
            f.write(t.isoformat())
        
    def load_timestamp():
        '''
        ISO formatted string loaded from a file. 
        '''
        while True:
            try:
                with open(TIMESTAMP_FILE_NAME) as f:
                    return datetime.datetime.fromisoformat(f.read())
            except FileNotFoundError:
                return None
            except ValueError:
                # parse error on file, delete and try again
                print('file corruption detected. recreating file...')
                os.remove(TIMESTAMP_FILE_NAME)
                continue
        
    def next_timestamp(current_date=None):
        if current_date is None:
            current_date = datetime.datetime.now()
        # get tomorrow's date
        next_date = current_date + datetime.timedelta(days=1)
        # ajust it for early in the morning
        next_date = datetime.datetime(
            year=next_date.year,
            month=next_date.month,
            day=next_date.day,
            hour=4,
        )
        return next_date
    
    def check_timestamp():
        '''
        Returns True at or after the date determined by next_timestamp.
        '''
        t = load_timestamp()
        
        # first time running, or missing file. create and return True
        if t is None:
            save_timestamp(next_timestamp())
            return True
        
        # file exists, check to see if it's a future time
        if t < datetime.datetime.now(): 
            t = next_timestamp(t)  # hasn't been run today, increment day to 6am
            save_timestamp(t)
            return True
        # already ran today, return False
        return False
            
            
    
    
    def show_error(msg):
        showerror('Error', msg)
        
    
    def init_tk():
        global root
        root = Tk()
        
        # configure our ttk styles
        s = Style(root)
        s.configure('Big.TLabel', font='times 40 bold')
        s.configure('Med.TLabel', font='times 25')
        s.configure('G.TLabel', font='times 20', color='red')
        
        # prevent tk window from popping up until we want it to
        root.withdraw()
    
    
    def get_wotd():
        '''
        queries masterrussian.com for the word of the day, translation, phonetics,
        and examples and returns them all as a dict.
        '''
        
        #return __TEST_WOTD
        
        url = 'http://masterrussian.com/blword.shtml'
        r = requests.get(url)
        r.raise_for_status()
        soup = BeautifulSoup(r.content, 'html.parser')
    
        wotd = {
            'word'     : soup.select('table h4')[0].text,
            'meaning'  : soup.select('div#wod_transl')[0].text,
            'phonetic' : soup.select('div#wod_pron')[0].text,
        }
    
        # examples are <li> tags alternating between a sentence and its translation
        # this code will get the block of <li>'s and group them as tuples
        examples = soup.select('ul.phrase_plain li')
        e = iter(examples)
        examples = [(next(e).text, next(e).text) for _ in range(len(examples)//2)]
    
        wotd['examples'] = examples  # add to our word object
        
        return wotd
            
    def wotd_cli(wotd):
        '''
        prints the word of the day out as formatted text meant for a CLI
        '''
        examples = wotd.get('examples', None)
        word = wotd.get('word', None)
        meaning = wotd.get('meaning', None)
        phonetic = wotd.get('phonetic', None)
        fmt = '''
        ########################################
        
        {word:^45s}
        
        ########################################
        =========
        {phonetic}
        {meaning}
        '''
        print(fmt.format(word=word, meaning=meaning, phonetic=phonetic))
        if examples is not None:
            print('\n----------------')
            for e,t in examples:
                print(f'{e}\n{t}\n---')
        
    def wotd_gui(wotd):
        '''
        displays the word of the day as a tkinter GUI
        '''
        global root
        root.iconify()
        WotdGui(root, wotd=wotd).pack(expand=True, fill=BOTH)
        root.mainloop()
        
        
    def main():
        '''
        check timestamp and display mode, showing the word according to whether 
        check_timestamp returns True, and prints to CLI if mode is '--cli',
        otherwise defaults to the GUI.
        '''
        import sys
        init_tk()
        
        mode = '--gui'
        if len(sys.argv) > 1:
            wotd = get_wotd()
            mode = sys.argv[1]
        else:
            if check_timestamp():
                wotd = get_wotd()
            else:
                return
                
        if mode == '--cli':
            wotd_cli(wotd)
        else:
            wotd_gui(wotd)
    
    
    
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
