---
title: ttty_menu
date: 2020-05-07
---
Example Python program ttty_menu.py

## Modules

* from Tkinter import *
* from tttk_menu import Menu
* from Tkinter import Menu as _Menu

## Classes

* class Menu(_Menu):

## Methods

* def __set_underline(self, kw):
* def add_cascade(self, cnf = {}, **kw):
* def add_command(self, cnf = {}, **kw):

## Code

Python tkinter example

    # coding: utf8
    
    u""" Tkinter::Menu クラスのカスタマイズ
    
    メニューのラベルに下線付きのショートカットを設定する場合、underline引数を指定し
    しないといけない……。
    
        menu_root.add_cascade(menu = menu_files, label = 'File', underline = 0)
    
    面倒ですね。gettextでメニューラベルを複数の言語に対応するのも、現実的じゃない。
    "&File" とか "File (&F)" とやりたいですよね。
    
    Example:
    
        from Tkinter import *
        from tttk_menu import Menu
    
        root = Tk()
        menu_root = Menu(mater = root)
        root.configure(menu = menu_root)
        menu_files = Menu(master = menu_root, tearoff = False)
        menu_root.add_cascade(menu = menu_files, label = '&Files')
        menu_files.add_command(label = '&New')
        menu_files.add_command(label = '&Open')
        menu_files.add_command(label = '&Save')
        menu_files.add_command(label = 'Save &As')
        menu_files.add_command(label = 'E&xit')
    
    """
    
    from Tkinter import Menu as _Menu
    
    class Menu(_Menu):
    
        def __set_underline(self, kw):
            if all(['underline' not in kw, 'label' in kw, '&' in kw['label'], ]):
                kw['underline'] = kw['label'].find('&')
                kw['label'] = kw['label'].replace('&', '')
    
        def add_cascade(self, cnf = {}, **kw):
            self.__set_underline(kw)
            _Menu.add_cascade(self, cnf, **kw)
    
        def add_command(self, cnf = {}, **kw):
            self.__set_underline(kw)
            _Menu.add_command(self, cnf, **kw)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
